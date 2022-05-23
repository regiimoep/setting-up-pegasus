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

## Step 2: Update Emulators

Dolphin MMJR and Citra MMJ both seem to have more up-to-date versions than the ones downloaded by Pegasus. You can find those on GitHub:
https://github.com/Bankaimaster999/Dolphin-MMJR
https://github.com/weihuoya/citra

## Step 3: Adjustment to 3ds Metadata.

The current Citra configuration has a slight issue. In order to run games off of Citra MMJ, you need to open the file `metadata.pegasus.txt` in the `3ds` folder.

In the `GamePath` parameter, replace `documenturi` with `path`.
![Adjust 3ds configuration](https://user-images.githubusercontent.com/106119828/169912444-f02e4948-a45d-4837-8292-40d1ba38d3af.png)

## Step 4: Organize your ROMs.

Before you go and put your roms onto your Odin, pause. We want to do the scraping still. For this, I recommend an external SSD or Hard Drive.
At first, I would go and copy the file system that the Odin created (the `roms` folder in the root directory of the internal storage) to your hard drive. From there, you can start importing your games into the respective folders. 

They are all adequately named, for example: 3ds games go into the `3ds` folder, etc.

## Step 5: Setting up SkraperUI

We want to use [Skraper](http://skraper.net/#download), which exclusively uses Screeenscraper.fr for the retrieval of data. It's able to read the file data an compare checksums in order to find the correct cover art, in case some files are misnamed. It also has a huge repository of Cover Art, Screenshots, and the like.

In order to use it, you need to first create an account with https://screenscraper.fr/. After that, load the SkraperUI executable and input your login data. After clicking "Validate", you can continue.

![SkraperUI](https://user-images.githubusercontent.com/106119828/169911323-cf823be5-e376-4ea7-bb31-b7cfe1332b50.png)

From there, you can continue. I used the "Generic Emulation" setting, as Pegasus does not use RecalBox (which I was previously used to)
![Generic Emulation](https://user-images.githubusercontent.com/106119828/169913019-3009cc5e-094f-41bf-97af-b5df6682c238.png)

Now, specify the folder in your hard drive containing all your roms and isos. It will detect the systems available and you can continue thereafter.
![Location of Your folder](https://user-images.githubusercontent.com/106119828/169913061-1a0bbd72-0d0d-47fd-a81b-82696552dc80.png)

Now, we get to the fun part. The themes that Pegasus uses make use of three different media types: Screenshots, 2D Boxarts and Wheels (basically the title images of the respective game). In the "All Systems" Setting on the left hand side, open the tab "Media", and in there, remove the preset media (Internal Mix and Manual) by clicking on the big images and clicking the "-" button to the left of the selection menu.

After that, click "+" and make the following setting:

Image - Screenshot


Click "+" another time and use Image - Box 2D


Click "+" a final time and use Image - Wheel

That is everything that needs to be set up. The folder should still read `%ROMROOTFOLDER%\media\xxxx` depending on what you chose. These are the locations Pegasus reads from, no need to change anything there.
![Media to Scrape](https://user-images.githubusercontent.com/106119828/169913370-90b93ca5-4bbf-463f-862c-beaf38beaffd.png)

You can now click the big run button on the bottom right side and let the scraping begin! It may take a while as Screenscraper's servers are not the fastest, but rest assured that most of you games will probably be found.

## Step 6: Manually adding Screenshots or Boxart

Sometimes, you want to use Romhacks or games that are unknown even to Screenscraper (rare occurence, but it happens). For these cases, you can now visit the `roms/[system]/media` folders and insert your own image files. **The only thing you need to ensure is that the image files are the same as the filename of your ROM/ISO!**

## Stzep 7: Move your folders

Now you're basically done with the initial setup + scraping. Move the folders to your Odin's internal storage, or put them into your SD Card. **Pay attention, as AetherSX2 is unable to run games from the SD Card, but running from internal Storage does work**.

**One more caveat: In my experience, it is not possible to run WBFS Wii Games from SD Card, it is therefore recommended to convert all games to either Nkit or ISO formats for proper compatibilty**.

## Step 8: Adding SD Card Folders to Pegasus

We have configured Pegasus to only read off of internal storage - No fun! This can be remedied by going into the Pegasus Settings. In there, you will find the "Set game directories..." option. Navigate one folder back and select the sequence of numbers that you find. This is your SD Card. 

From there, navigate to the folder where you moved the files from your Hard Drive to. For me, it was the `roms/[system]` folder still. There, you will find the `metadata.pegasus.txt` that you got from running Pegasus. Click on it, and the folder will be recognized. Repeat this process for all folders that are now located on your SD Card. 

After exiting the menu, Pegasus will ask you if you want to reload the game list - Confirm. Pegasus will then proceed to reload and you should see all of your games, scraped and ready to go!

You can now freely switch between themes and see what fits your taste best.

## Step 9 (optional): Adding new cores to Pegasus

You can also add new systems to Pegasus that are not part of the initial setup. For that, I recommend you use the same folder as you used previously.

Create a new folder for the system you want to use and give it a fitting name. My example here is "easyrpg" as I want to play some RPG Maker games.

Visit https://pegasus-frontend.org/tools/metagen-android/ and find the system you want to emulate, click it and copy the text appearing on the right hand side into a newly created `metadata.pegasus.txt` file of your own making.

After that, you can paste your games and either scrape or add your images on your own. Make sure to use the same folder structure as Skraper gave you. (`media/box2dfront`,`media/screenshot`, `media/wheel`).

You can then repeat the process described in Step 8 to add the new folder to the collection. 

## Step 10 (optional): Ignoring unnecessary files.

You may notice that sometimes, games come up multiple times. That is especially the case for older CD-based games (PC Engine CD, PSX, etc.). This is because Pegasus recognizes all potential formats a game can be. For PSX, that is for example `cue, bin, iso, etc.`. This can be remedied by going into the respective `metadata.pegasus.txt` and editing the file extensions to listen to in the folder.

For example, I created `.m3u` files for all of my PSX games and ignored all other file extensions by adding an `x` to them in the metadata file:

![image](https://user-images.githubusercontent.com/106119828/169914927-0909d4e3-5664-4d98-8ea1-1aa702b0df47.png)


Use the File names you want to run in the `.m3u` file. You can use any text editor to create them.

![image](https://user-images.githubusercontent.com/106119828/169915010-5c1cc3d5-3a2a-4a72-ba0b-e0cf44a8e5b7.png)
Example for an edited metadata file.

For other systems, it may simply suffice to invalidate a few file extensions. In my case, this was possible for PC Engine CD.

## Step 11 (not optional) - Enjoy playing!

You're all set! Enjoy your Odin and the awesome new frontend you're now able to make use of! :)
