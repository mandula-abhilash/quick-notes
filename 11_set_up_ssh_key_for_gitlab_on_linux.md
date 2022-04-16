## Install Git

`sudo apt-get install git`

`git --version`

## Configuring git

``` 
git config --global user.name "Abhilash Mandula"

git config --global user.email "mandula.abhilash@gmail.com" 
```

## Generating an SSH key

ssh-keygen

![image](https://user-images.githubusercontent.com/77572066/163672367-02913355-ebe3-42bf-b5e5-830b6ac4937f.png)

## Adding your SSH key to GitLab

cat /home/abhilash/.ssh/id_rsa.pub

Follow the below steps: 

 - Copy the entire contents of the file.
 - In GitLab, go to your profile settings [SSH Keys](https://gitlab.com/-/profile/keys).
 - Paste the key and give it a name

If username/password is still being asked, then check if the clone url is https or ssh. SSK keys work only if the clone url is ssh

```
$ git remote -v
  origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
  origin  https://github.com/USERNAME/REPOSITORY.git (push)
```

Change your remote's URL from HTTPS to SSH with the git remote set-url command.

```$ git remote set-url origin git@github.com:USERNAME/REPOSITORY.git ```

