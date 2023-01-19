# 🐍 tailchat

Possibly a quite recklessly basic chatting app, built for lizard communication 🦎.

Built on [Vue.js](https://vuejs.org/) and [Pocketbase](https://pocketbase.io/), "Tailchat" follows in the footsteps of [dyablog](https://github.com/0xBA5E64/dyablog) as my second adventure into more dynamic web development, all but guaranteed to be shock-full of beginner mistakes and security blunders. A trial by fire I hope it will be, for this winter has been especially harsh for us ectotherms.

## Project Setup

This project uses [Vite](https://vitejs.dev/) for running its frontend and [Pocketbase](https://pocketbase.io/) for the backend, both should be run simultaneously in separate shells *(because I don't know yet know how this is supposed to work, barring bringing in tmux as a vital part of your server architecture)*

## Clone and enter the repo

```
git clone https://github.com/0xBA5E64/Tailchat.git
cd Tailchat
npm install
mkdir backend && cd backend
wget https://github.com/pocketbase/pocketbase/releases/download/v0.11.3/pocketbase_0.11.3_linux_amd64.zip
7z x pocketbase_0.11.3_linux_amd64.zip pocketbase
rm pocketbase_0.11.3_linux_amd64.zip
```


### Compile and Hot-Reload for Development

```sh
npm run dev
# And, in a seperate shell simultaniously:
npm run backend
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```
