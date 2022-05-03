# WORKSPACE_SETUP
###### tags: `Workspace` `Robot` `Setup`
[ToC]
## Virtual Machine VMware
[:point_right: vmware workstation player download page](https://customerconnect.vmware.com/en/downloads/info/slug/desktop_end_user_computing/vmware_workstation_player/16_0)
* ### Ubuntu 18.04版本
    > Ubuntu 18.04.6 LTS (Bionic Beaver)記得下在long term surport的Desktop image版本
    > https://releases.ubuntu.com/18.04/
* ### Virtual Machine Settings
    | Features             |    Set to               |
    | -----------------    |:----------------------- |
    | 1. memory            |                         |
    | 2. processors        |                         |
    | 3. hard disk         |                         |
    | 4. network adapter   | Bridged                 | 
    | 5. display           | uncheck Accelerate 3D grahics |
    4. network adapter :
        > 為了後續Ros使用TCP/IP，不會跑錯需將Network Connection改成Bridged模式，此舉的目的是讓虛擬機與主機有相同等級的ip
    5. display :
        > 避免Gazebo跑錯，不可使用accelerate 3D grahics
## Work Environment
* ### 建立好用的CLI
    1. check environment
        ```shell=zsh
        echo $0 
        # 先確認預設shell(通常為bash)

        zsh --version 
        # 確認電腦上沒有zsh
        ```
    2. download zsh
        ```shell=zsh
        sudo apt-get update && sudo apt-get dist-upgrade -y
        # 更新software和security patches

        sudo apt-get install build-essential curl file git
        # 確保有1.build-essential 2.curl 3.file 4.git

        sudo apt install zsh
        zsh --version
        # 下載zsh，確認下載成功

        which zsh
        # 確認位置，預設為/usr/bin
        ```
    3. change login shell
        ```shell=zsh
        cat /etc/shells
        # 查看已經下載可運行之shells
        # 其中包含 which zsh 指令所顯示之zsh位置

        chsh -s $(which zsh)
        # change login shell的指令
        # 需要reboot
        ```
    4. ignore zsh config setup
        ```shell=zsh
        # 打開terminal會有歡迎介面，並且要求你設定基本configuration
        # 不使用任何設定(oh-my-zsh有預設)
        ```
    5. oh my zsh
        ```shell=zsh
        sudo apt install git-core curl fonts-powerline
        # 確保有1.git-core 2.curl 3.fonts-powerline

        sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
        # 下載oh-my-zsh
        ```
    6. oh my zsh plugins
        ```shell=zsh
        # 對照github上的.zshrc
        # https://github.com/jerryhuangyu/zshrc/blob/master/zshrc
        # 加入plugins，發現缺少

        # zsh-autosuggestions
        git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

        # zsh-syntax-highlighting
        git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

        # autojump
        git clone https://github.com/wting/autojump.git
        # 進入資料夾執行install.py(可能需要先下載python-is-python3)
        ```
    7. p10k
        ```shell=zsh
        # 需先手動下載字體
        # https://github.com/romkatv/powerlevel10k#manual-font-installation

        # 接著下載p10k
        # https://github.com/romkatv/powerlevel10k#oh-my-zsh
        git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

        # Set ZSH_THEME="powerlevel10k/powerlevel10k" in ~/.zshrc.
        ```
    8. apt install
        ```shell=bash
        sudo apt install tree
        sudo apt install python-is-python3
        sudo apt install htop
        sudo apt install locate
        sudo apt install trash-cli
        sudo apt install neofetch
        ```
    9. plugin
        ```shell=zsh
        python
            # mkv [name]
            # vrun [name]
            # deactivate
            # pyfind
            # https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/python
        ```
        ```shell=zsh
        pip
            # this plugin adds completion for pip, the Python package manager.
            # https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/pip
        ```

- ### VScode

    - setting
        > ctrl + , 
        > \# go to settings
        > \# search: editor bracket pair (為括弧等..上色)

        ![](https://i.imgur.com/Ry8x51H.png)
        > \# search for: word wrap (自動換行)

        ![](https://i.imgur.com/seI3Rcr.png)

    - theme
        > ctrl + k + t
        > \# night owl
        > \# cobalt2
        > \# shades of purple
        > \# coder coder dark
        > \# codestackr

    - extenstion
        > \# prettier (auto format your code)
        > \# auto rename tag (同步更改前後tag)
        > \# vscode-icon
        > \# fluent icons
- ### Chorme (option)
    [chorme download page](https://www.google.com/chrome/?brand=JJTC&gclid=EAIaIQobChMItMSS8fLC9wIVgQh9Ch2XLQ2OEAAYASAAEgJx1vD_BwE&gclsrc=aw.ds)
- ### Uninstall firebox (option)
    ```shell=zsh
    sudo apt-get purge firefox
    ```
    [more info for uninstall firebox](https://technastic.com/uninstall-and-install-firefox-on-ubuntu/)
## Install ROS
1. Configure your Ubuntu repositories
    ![](https://i.imgur.com/Myx5ofq.png)

    ![](https://i.imgur.com/nVV0FNI.png)
    search software updater
    
    ![](https://i.imgur.com/cVem00a.png)
    Configure your Ubuntu repositories to allow "restricted," "universe," and "multiverse".
    [more info on config repository](https://help.ubuntu.com/community/Repositories/Ubuntu)
    

1. Setup your sources.list
    ```shell=zsh
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    ```

1. Set up your keys
    ```shell
    sudo apt install curl # if you haven't already installed curl
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
    ```
1. Installation
    ```shell=zsh
    sudo apt update
    sudo apt install ros-melodic-desktop-full

    # install a specific ROS package
    sudo apt install ros-melodic-PACKAGENAME
    # To find available packages, use:
    apt search ros-melodic

    ```
3. Environment setup
    ```shell=zsh
    echo "source /opt/ros/melodic/setup.zsh" >> ~/.zshrc
    source ~/.zshrc
    ```
5. Dependencies for building packages
    ```bash
    sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
    # initialize rosdep.
    sudo rosdep init
    rosdep update
    ```
7. Build farm status
    >The packages that you installed were built by the ROS build farm. 
    [check status of individual pkg](http://repositories.ros.org/status_page/ros_melodic_default.html)

## Github Account
> 用於程式碼之版本管理



