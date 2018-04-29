# Expanding RAID using ArecaCLI

It's extremely easy to expand a RAID set on Areca RAID cards. I have an ARC-1261 - however all the Areca cards have the same interface and use the same management software. Good stuff! It's just a pity there isnt a standard for hard RAID management in Linux/FreeBSD like there is in OpenBSD. Areca is possibly the best raid card for OpenBSD but regardless, a note of warning... these steps may help you on Linux, FreeBSD and Windows but not in OpenBSD.

So yes this is how I have expanded my RAID 5 array in FreeBSD using the areca-cli command line management tool.

There are four steps. Three of which are in the Raid card, the third is OS level

## Step 1
Plug in a new drive. Ideally it should be the same as the other drives in the candidate RAID set. Turn on your computer, assuming it boots to your OS successfully. Go to the command line and run `arecacli` then go it your admin password with `set password=0000`.
<pre># ./arecacli
# set password=0000
</pre>
Now type `rsf info` and check that your raid array is *healthy*, that is that the *State* is *Normal*. Then check that the new disk is present with `disk info`. If your raid array isn't optimal and the new disk isn't present... well go fix it :) The new disk should have a *Usage* of *Free*.

## Step 2
From the two info commands in Step 1 you will know the raid set number (left most column of the info output) and the disk number (again, the number in the left most column of the info output). We can now expand the raid set with the following command:
<pre>rsf expand raid=1 drv=13</pre>
Noting that *raid=1* refers to the raid set not the raid level! So where I have `raid=1` you should use the raid set number on your local machine that we found in Step 1, and similarly where i have `drv=13` you should use your disk number. If you run `rsf info` again, you will see that the *State* is now *Migrating*. This will take some time and you can see the progress as a percentage with `vsf info`. You can speed it along considerably by increasing the background task priority with `sys changept p=3`, remember to set that back to `1 (Low)` when you're done.

## Step 3
Expand the volume set (more details here)

## Step 4
Expand the partition and filesystem. This is specific to your operating system. I won't provide details here except to say that in FreeBSD one uses the `growfs` command, and if you formatted the drive raw rather than slicing/partitioning it (yes you can do that in FreeBSD) then there is no need to worry about enlarging the slice/partition.

It does take some time (days), but it can continue if you shut down the computer and you can continue to use the file-system while its expanding (albeit more slowly)
