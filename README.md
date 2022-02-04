# Conda-Trick-42
How to install conda / python and avoid space problemss, the install wil be saved to sgoinfre and moved back to goinfre for speed.   
<br></br>

## WARNING  
This is just a fix of mine and i have no clue if this will work as intended, be carefull.  
<br></br>

## Explanation
As you know sgoinfre and goinfre have space, and we need space, but what's the difference ?    
**goinfre** is on the physical computer, and will disapear when you change places.
**sgoinfre** is on the servers and will not dissapear.

<br></br>
## Why goinfre ?
You can install conda on sgoinfre and never have problems but **IT WILL BE SLOOOOOW**.   
My solution ? copy the files from sgoinfre to goinfre every day (go have a coffee i guess :) ) and have the path point to ~/goinfre/miniconda so it will work.

<br></br>


# How to ?

First install miniconda in goinfre (say yes to everything, including conda init):

```bash
cd ~/goinfre
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -p $(pwd)/miniconda
```
<br></br>
Now we need to add conda to the path, so we add the following line to .zshrc (or.bashrc) above the `# >>> conda initialize >>>` line:
**change YOUR_USERNAME with your real username!!** 
```bash
export PATH=$PATH:/mnt/nfs/homes/YOUR_USERNAME/goinfre/miniconda/bin
```
Then install the python libraries you need:    
**JUST INSTALL WHAT YOU NEED, THIS IS A DATASCIENCE AI INSTALL FOR EXAMPLE**
```bash
conda install pytorch torchvision torchaudio cpuonly -c pytorch
conda install -c conda-forge jupyterlab
conda install -c conda-forge numpy
pip   install    pillow
```
If you get a `conda command not found either the install failed, or you forgot to restart your terminal`. 
<br></br>

Now we copy the install files to sgoinfre so they dont get deleted. The progress % is wacky but it should go to 2-4GB and take about 10 minutes.    
**If you install new packages later and dont want them to dissapear when u change computers you will have to run this again,** it will only copy modified files and wont take long the second time.
```bash
rsync -ah --info=progress2 ~/goinfre/miniconda ~/sgoinfre
```

and now you can work as you like. If you go to a new pc copy your files from sgoinfre to goinfre again with;

```bash
rsync -ah --info=progress2 ~/sgoinfre/miniconda ~/goinfre/miniconda
```
this should take about 3 minutes

## Sanity Check ?
If your install is good and running `which python` should output `blabla/goinfre/blabla`

