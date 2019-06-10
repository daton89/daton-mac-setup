# Windows with WSL

Recent macbooks are quite expensive and you can't change any part. 

So I recently bought a Dell XPS 15 9570.

I found this machine really the coolest I've ever had, and with the recents version of windows you can really take advantages of Unix systems for development, thanks to WSL \(Windows Subsystem for Linux\).

I would give to Windows another changes to be my OS for my development enviroment. 

After enabled WSL into Windows Features, opening a terminal you'd be able to run linux natively with: 

```bash
wsl
```

A Store window will be opened and you will be able to choose a Linux disto, I'm using Ubuntu.

After a few minutes, we'd be able to open start and click on Ubuntu, a new cmd will be opened and TAAADAAA... we have a bash... so create a new user and we're ready to go!

## Troubleshooting

I reccomend to install git and add to Path env variable the `C:\Program Files\Git\bin` path, so that the `bash` and `sh` executables are available in case some software require it \(like pm2\)



