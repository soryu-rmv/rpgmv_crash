# Tips to save our project data from RPGMV crash

by @soryu_rpmakermv

-------------------------------------------------

<br>

## 1. Introduction

RPGMakerMV has potentially unstable behavior after it has been roled out in 2015.  
The most significant feature of RPGMV is its portability for various platforms.   
Instead, several faults in RPGMV editor are seen which were hardly in previos series of RPGMakers.   

What I worry the most is high frequency of crash and force termination of RPGMV.   
Though number of items in database which can be handled in RPGMV editor got fewer compared to old series,   
we often encounter force termination of RPGMV when we are using almost maximum items in the database.
Especially, termination during the save of current working project is tragedy, which devastates the data file at worst.   

![json](https://user-images.githubusercontent.com/64351233/80788333-c5b3cd00-8bc3-11ea-9d11-bd549341cf43.png)   

Above figure shows a dialog which notifies that Animations.json has been destroyed    
after force termination of RPGMV has occurred. In this time, Animations.json becomes empty.
We never open RPGMV game project unless we fix Animations.json for designated format.   
Even if we succeeded to open a project, we hardly can restore the animation data without its copy in advance.   

When we launch RPGMV, RPGMV extract data (events, playing bgm, map data, database, and so on)     
from every .json files into memory (Here, memory is a space allocated for RPGMV to save project data.)     
until it is terminated. Note that, items in database are also written in corresponding files 
as the project is saved **even if there are no changes in database**.     

Installing additional physical memory into our PC absolutely does not help this behavior.    
We never can fix the problem in RPGMV by using js plugins. Only we can do is just waiting.    
However, it is not still fixed after more than 5 years passed when RPGMV is released.
On the contrary, the developement has been already directed to another maker series such as     
Visual Novel Maker and Pixel Game Maker. Actually, RPGmakerMV is poted to PlayStation 4 and   
Nintendo Switch as "RPGmakerMV Trinity" in Japan, which has been condemned by purchasers due to serious bugs in a editor.



During my works with RPGMV, I have experienced many times of force termination and being destroyed data    
and lost much time for the work. I was greatly disappointed as if I heard a revelation that   
"RPGMaker MV is not a tool for making professional RPGs". To defy this damned situation,    
I began to consider methods of self-protection for current working project data from frequently causing RPGMV crash.   




<br>

## 2. Situation RPGMV crashes
First, I enumerate several situations which RPGMV was force terminated in my works.

- When the current working project is saved
- When I push **"OK"** in the window of making events and Database
- During I make events (Operations for the choice of Event Commands)
- Any constructions **with playing bgm by using SoundTest in RPGMV**

Of course, data destruction due to an error during project saving is out of the question.   
It is also a matter that termination while making events gives no choices for us to save working data.   

<br>

## 3. Countermeasures

### 3.1. Migration of database files which have large number of items temporary 

If we encounter destruction of Animations.json frequentyly, it is a considerable choice that   
we make Animations.json empty on purpose with the migration of original Animations.json file.     
However, as I mentioned first, RPGmakerMV cannot open a project with completely empty Animations.json file.     
We then have a preparation as follows.   

- 1. Rename a file ./data/Animations.json in current project to appropriate name or copy to any other directories.
- 2. Delete all animation data in Database in RPGMV（Let Animation lists be empty.）.
- 3. Save a project（You may exit RPGMV here once.）.
- 4. Have a copy of Animations.json (This is now almost empty.), rename it as Animations_.json for example.
- 5. Open RPGMV （Animations.json which is an almost empty file is loaded.）

<br>

![animations](https://user-images.githubusercontent.com/64351233/80791751-92763b80-8bcd-11ea-8d2e-072a3610efbc.png)


Above figure is an example to do that. When we make animation data to upper limit in RPGMV editor,    
The size of Animations.json reaches to about 10MByte. However, your work is to design events     
(for example) conversations among characters, Animations.json is no need unless showing animations.   
In this case, the risk of force termination in RPGMV is decreased by loading almost empty Animations.json file.   
Moreover, the loading time of projects can be shorten.    

<br>

When you need to test play including battles, **place genuine Animations.json (Have you migrated it before, right?)**   
**file at ./data/ in your project again**.    
Do not forget to escape dummy Animations.json, or you have to make it again in RPGMV.    



<br>

Though we take it for granted that the copy for backup is taken in daily working,   
there is no such thing as doing too much countermeasures for RPGMV because it is somehow wicked than we expect.    
(Losing just a few animation data make us sad, and require additional working cost to restore them.)     

<br>


While we use RPGMaker with dummy Animations.json, the target of "Show Animation" commands in events is   
displayed as  **？** .　You never mind this because it is not our fault.    
Configration of showing animation in events on a map is saved in its map file named MapXXX.json.  
After we place genuine Animations.json (and reload RPGMV), it is immediately restored.  


<br><br><br>

### 3.2. Refrain to play songs in RPGMV 

Playing songs in RPGMV thourgh SoundTest, the data of sound file is exactly stored into memory.  
As it depends on file size (or bit rate and duration of songs), we sometimes fail to play magnificent songs   
with long duration. It is so convenient for us to check song loop for ogg files by using RPGMV SoundTest.    
But, working for RPG making with playing songs in RPGMV leads to risk of force termination of RPGMV.  

**If you just want to songs as BGM, it is better to play not by RPGMV but other tools**.   

<br><br><br>

### 3.3. Have a copy of created events for backup before saving project

We feel fear when we think that "I wanna save but the save may crash!!".
In particular, after finishing a grate scale of event scenes, the process of save is something like lottery.   
(We need strong brave to start save.)   



Then I suggest to **launch another RPGMV** before saving the project.    
The execution of RPGMV as soon as it has just been launched almost never die. (Of course,    
additional memory is required to run multiple RPGMakerMV. It may be hard for those who are using old PC.)    


<br>

Fisrt, just Launch **another RPGMV**.  
Below figure shows that two RPGMV are aligned. The left one is that I have been working (just finished an event),    
and the right one is additional RPGMV.  

![rpgmv2](https://user-images.githubusercontent.com/64351233/80798983-9a8ba680-8be0-11ea-82f3-67c7820adac8.png)

It is important that **events and other items in RPGMV can be copied beyond its window**.  
Furthermore, they can be copied to different maps in another RPGMV window.   
In addition to this, they can be copied to different RPGMV game projects beyond the window.   


Based on this, we attempt to copy an event which is designed just now.  
We can copy any items in RPGMV by Ctrl+C shortcut or choicing Copy from right click.  
After the item is copied, **paste it into another RPGMV window**.   
(In terms of efficincy of works, it is better to copy between the same maps.)  
We also can paste in RPGMV by Ctrl+V shortcut or choicing Paste from right click.  

After that, attempt to save in the original RPGMV window.   
If the save is succeeded, it is no problem to close the another RPGMV.    
If you failed, the another RPGMV helps you to restore the event immediately.   
(Even if you succeeded, it may be better to restart RPGMV to continue additional events making.)

<br><br>

Note that
- you never proceed the work with both RPGMV windows, or there is a risk to lose consistency of your project data,
- and it is no problem to launch multiple RPGMVs as long as to only **load the data**.

