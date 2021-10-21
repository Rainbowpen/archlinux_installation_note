# User and config
This will help my life a bit easily 

## User

- Add new user
- Add user to group
- Make sudo work

### Add new user

    $ useradd "username"

### Add user to group
You might want use sudo or docker etc...

    # e.g.
    $ usermod -aG "groupname" "username"

    # sudo (group name will call sudo or wheel depend on you)
    $usermod -aG wheel heymynameissimon

    # docker
    $ usermod -aG docker heymynameissimon

### Make sudo work
Edit /etc/sudoers, find this line and uncomment
    
    #%wheel ALL=(ALL) ALL

If you want to use sudo without password

    %wheel ALL=(ALL) NOPASSWD: ALL

## Config
This is option, depend on what program you need,
find some example and put it in to ~/.config.

Or clone this [repo](https://github.com/Rainbowpen/quick-dotfile.git) and pick what you need.


---


Click here back to [home](./README.md) page.
