Arionum mining on VM
==================

This is a quick tutorial for those wanting to mine Arionum on a virtual machine. You can use Vultr for this purpose and setup a Ubuntu 16.04 VM.

If you are interested in signing up on Vultr too, you could use my [ref link](https://www.vultr.com/?ref=7436414) to sign up. Otherwise just browse to [Vultr](https://www.vultr.com) and sign up.

If you need help setting up a VM, contact me here.

After your VM is setup
-------------

You can setup your VM to include SSH keys such that you can SSH into your VM from a remote location. See this great guide on how to do that: [Guide](https://www.vultr.com/docs/how-do-i-generate-ssh-keys).

Once you are in, there is a couple of commands you need to run.

    sudo apt-get update
    sudo apt-get install openjdk-8-jdk maven git gcc make -y
    sudo apt-get install build-essential -y
    cd 
    git clone https://github.com/ProgrammerDan/arionum-java.git < "/dev/null"
    cd /arionum-java/arionum-miner
    git checkout investigate
    touch config.cfg
    chmod 755 config.cfg
    echo "pool
    http://aropool.com/
    dASeyY4Acp2iR1bToLJxVpfsjjXTivpe22A3nA8jeFAMVAHusMmp8s4M67UnpVPxES3D9TFyYCvEGhxxSsDKhVu
    `nproc`
    enhanced
    true
    `hostname`" > config.cfg
    mvn clean package
    chmod +x build-argon.sh
    ./build-argon.sh
    chmod +x run.sh
    
Please make sure to adjust the address to yours!


If you want to be able to check what your miner is doing, I.e. see all the log output, hashes etc. run the following now:

    sh run.sh

If you would like the miner to run in the background, install tmux and start the miner in a new tmux session.

    sudo apt-get install tmux -y
    tmux new-session -d -s my_session 'sh run.sh'
    
You can now close your session and the miner will continue running within the tmux session.
At a later stage, you can check your session / miner using the following commands:

    tmux list-sessions 
    
This lists out all tmux sessions currently running.

To actually see what is running in those sessions you have to attach to the particular session, to do this:

    tmux attach -t n (where -t stands for target session and n for that session number).

