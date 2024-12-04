# README

## 3.a The commands to any downstream developer to setup and operate your submission.

To run this application dockerized you can run 
```
docker-compose build && docker-compose up
```
* this command will build the Dockerfile, raise the application and create the necessary volumes.
* it doesn't run the necessary migrations from spina, so you need to initialize it. To do so you need to exec into `yourwebsite-demo-web`container and run
```
rails spina:install 
```
* since you need to input some information into it and it's run only once. I belive it's a acceptable start.
## 3.b Brief description of key challenges and goals of your submission.

* The biggest challenge in this task was to setup my environment:
  * One of my issues was related to mac's latest update `sequoia 15.1.1` which disabled the CPP compiler, making it impossible to install `sassc` one of `spina`'s dependencies solved by [git comment](https://github.com/sass/sassc-rails/issues/182#issuecomment-2453222192) .Editing `rbconfig.rb` and enabling `CONFIG["CXX"] = "clang++"`
  * Also had many compatibility issues with `sassc`, `rails`, `spina`. One that took me some time was:
  ```
  ActionView::Template::Error (undefined local variable or method `javascript_importmap_shim_nonce_configuration_tag' for #<ActionView::Base:0x000000000109c8>):
  ```
  * which didn't made much sense to me since the `importmap` doesn't seems to have support to rails lower to 7 which was the version I was running and the version I saw in a bunch of tutorials.
* Had a small issue initializing the database and running migrations, which I don't think is a huge issue since you initialize the database once, so seems fair to run commands from the container.

## 3.c It’s okay to call attention to areas that you aren't certain about and might make different choices if you took more time

* Regarding the parts that I'm used to working on (docker, docker-compose) to me things seem fine.
   * One point to improve docker build time, using some sort of node cache and creating a base image to use with most things installed.
* the lack of knowledge debugging ruby proved to be a big issue for me in this challenge, took some time to understand a few issues mainly because a bunch of them seemed to be related to internal things from SpinaCMS and should be a simple plug n play.
* One point to improve in this project is move the .env file from the repo to a secure place since it contains DB password and ruby master key.
## 3.d Note any known caveats and potential failure scenarios downstream developers may experience.
* Had problems re-running database migrations. So I belive it's a possible failure point. 
  
## Conclusion

Most of my issues while working on this task came from setting up the environment and not knowing if things were working correctly. Also adding to it building this docker was extremely slow mostly due to the preload which is annoying to improve on. After using the correct versions from packages things seem to get in place just fine, By the way, I found it a little amusing that when creating a new project ruby changes my rails version.