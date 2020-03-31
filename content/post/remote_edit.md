+++
title = "How to remotely edit your project without having to use VIM"
date = 2019-04-09T15:20:37+08:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Handuo"]

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Network", "Tools"]
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = "codeserver/codeserver.png"
caption = ""
preview = true
preview_only = false


+++

Remotely editing your work when your server does not have public IP address and you don't want to spend any money is not so easy. Maybe you can use Team viewer or Anydesk or even chrome remote desktop, but there are high latencies. Maybe you can use ngrok to remotely ssh to your server, you have to use vim and you are not familiar with it at all :anguished:. I tried to use rmate but it is not convinient to edit across different files in a folder.

I recently found an hot github repository called [code-server](https://github.com/codercom/code-server) which is able to run **VS Code** on a remote server, accessible through the browser. So it suddenly came to my mind that I can remotely edit any code for free as long as I have a linux/macOS environment. 

Let's consider you understand the basic knowledge of SSH key as you are going to use it. For tutorial about how to generate SSH keys, please refer to [How to set up SSH keys](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2) and [connecting to GitHub with SSH](https://help.github.com/en/articles/connecting-to-github-with-ssh).

Firstly you need to see whether your server has a public IP address. If yes (I know this is not common), then things are really easy and you can just follow step 1, 2 and 3; otherwise, directly go to step 0, then step 2 and 3.

## Step 1. SSH connect
```
ssh server_username@IP_address -L 8843:localhost:8843
```
The `-L 8843:localhost:8843` here is **local port forwarding** which allows you to access local network resources that aren't exposed to the Internet. The first 8843 is local port, `localhost:8843` is the remote **code-server** default port.

To see whether you can successfully links to the server. The prerequisites are 1) you installed openssh-client 2) you have generated SSH key. If not successfully, maybe you don't have a public IP address. Then go to step 0.

## Step 2. Download code-server
Open this page on your client browser, find the latest release of [code-server](https://github.com/codercom/code-server/releases). Find the binary file for linux and get the downloading address. ![Download binary file](/img/codeserver/download.png)

Then in the terminal window ssh connected to the remote server, type:
```
wget code-server_downloading_address
# Example:
wget https://github.com/codercom/code-server/releases/download/1.696-vsc1.33.0/code-server1.696-vsc1.33.0-linux-x64.tar.gz
tar -xvzf code-server1.696-vsc1.33.0-linux-x64.tar.gz
cd code-server1.696-vsc1.33.0-linux-x64/
sudo mv code-server /usr/local/bin/
```
Then your **code-server** will be installed!

## Step 3. Running code-server
Go to the folder of your code waiting to be edited and type `code-server` in the terminal window ssh connected to remote server.
Then open your browser and type `localhost:8843`, your workspace of VSCode will be revealed to you! The speed is satisfactory to me.

## Step 0. Ngrok

Some people will use VPS servers or cloud hosting providers like [Vultr](www.vultr.com), AWS and so on to pay for a public IP address. But here we just need [Ngrok](www.ngrok.com), a great tool that can create a tunnel from the public Internet to a port on your local machine. You can give this URL to anyone and any place without the need to pay any money!

Download ngrok onto your remote server and throw the binary file into /usr/local/bin/. Maybe need to `sudo chmod a+x ngrok`.
Then type:
```
ngrok tcp 22 --region ap
```
where --region refers to your region. There are four region options: us(Ohio), eu(Frankfurt), ap(Singapore), au(Sydney). If you don't select a region, the default one is us, which might be slow if you are in Asia.

Then your screen will show something like this:
![ngrok](/img/codeserver/ngrok.png)

There is a number after `0.tcp.ngrok.io:` **15707**. You need to remember this port number. Please keep this window on if you want to keep this tunnel open.

Then you can ssh to your remote server by copying the command:

```
ssh hd@0.tcp.ngrok.io -p15707 -L 8443:localhost:8443
#Or your region is ap
ssh hd@0.tcp.ap.ngrok.io -p15707 -L 8443:localhost:8443
```



