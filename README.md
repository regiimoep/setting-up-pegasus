# Extended Setup Guide to setting up Pegasus on Odin

This describes my process of setting up Pegasus on Odin, with big files (except for PS2) located on my SD, whereas the rest is on my Odin directly.

## Step 1: Running Pegasus Installer

The first step should be obvious.
* Install Termux
* Allow it to install files from unknown sources in settings
* Run `/bin/bash -c "$(curl -fsSL https://bit.ly/3ntlzL8)"` on Termux
* Follow the guide to designate you have on Odin
* Use "Internal Storage" as the default for the roms-folder location. You can later move folders to the SD Card.
* When asked if you want to scrape your games, don't! We'll do that on our PC

## Step 2: Organize your ROMs.

Before you go and put your roms onto your Odin, pause. We want to do the scraping still. For this, I recommend an external SSD or Hard Drive.
At first. I would go and copy the file system that the Odin created (the `roms` folder in the root directory of the internal storage) to your hard drive. From there, you can start importing your games into the respective folders. 

They are all adequately named, for example: 3ds games go into the `3ds` folder, etc.

## Step 3: Adjustment to 3ds Metadata.

The current Citra configuration has a slight issue. In order to run games off of Citra MMJ, you need to open the file `metadata.pegasus.txt` in the `3ds` folder.

In the `PATH` parameter, replace `documenturi` with `path`.
![Adjust 3ds configuration](https://user-images.githubusercontent.com/106119828/169912444-f02e4948-a45d-4837-8292-40d1ba38d3af.png)


![SkraperUI](https://user-images.githubusercontent.com/106119828/169911323-cf823be5-e376-4ea7-bb31-b7cfe1332b50.png)
