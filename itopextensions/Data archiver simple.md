1. # Data archiver simple

   - name:

     Data archiver simple

   - description:

     Archive tickets from the console

   - version:

     1.0.1

   - release:

     2017-10-31

   - itop-version-min:

     2.4.0

   - download:

     https://store.itophub.io/en_US/products/combodo-archive-manual

   - code:

     combodo-archive-manual

   iTop is getting slow due to a **high volume of tickets?**
   You would like to get rid of them, but… what if a customer claims for an old ticket?
   Install this extension and you will gain performance, without loosing data.

   ## Features

   Improve performance when searching for a Ticket, if your outdated Tickets represent much more than the active ones, but cannot be deleted.

   - Allow administrators to bulk flag outdated Tickets as `Archived`
   - Hide `Archived` Tickets to all users most of the time, as if they were deleted.
   - But still enable them to retrieve `Archived` Tickets if needed.

   ## Revision History

   | Version | Release Date | Comments                |
   | ------- | ------------ | ----------------------- |
   | 1.0.0   | 2017-11-02   | First published version |

   ## Limitations

   Bulk archive/unarchive does not record the change in the object change history, whereas archiving/unarchiving a single object does record the information in the change tracking.

   ## Installation

   Like any other extensions, unzip it into **extensions** directory and relaunch the setup…

   ## Configuration

   *There is no configuration for this module.*

   ## Administrator experience

   When you have deployed this extension, then Tickets objects can be massively archived (and unarchived) by administrators only.

   Search for the Tickets that you want to Archive and from that list, open the **Actions** menu. Below two possibilities, in standard mode (only mass archive action available) and in archive mode (both mass archive and unarchive actions available)

   ![archive_manual_-_standard_mode_menu_list.jpg](https://www.itophub.io/wiki/media?media=extensions%3Aarchive_manual_-_standard_mode_menu_list.jpg)![archive_manual_-_archive_mode_menu_list.jpg](https://www.itophub.io/wiki/media?media=extensions%3Aarchive_manual_-_archive_mode_menu_list.jpg)

   Mass archive or unarchive actions sends to a confirmation screen :

   ![img](https://www.itophub.io/wiki/media?w=600&tok=a08808&media=extensions%3Aarchive_manual_-_list_confirmation.jpg)

   You can also do it on a single ticket details screen, using the **Actions** menu:

   ![img](https://www.itophub.io/wiki/media?w=200&tok=2ab0c3&media=extensions%3Aarchive-single.png)

   Both single object archive and unarchive actions are done without confirmation.

   ## End User experience

   ### In standard mode

   All archived objects are hidden, for all users including admins, like if they were deleted.

   A reference to their friendly name can be found in other objects pointing to them. Example on an archived contact which is the caller of a non-archived Change.
   ![Toggling menu](https://www.itophub.io/wiki/media?w=300&tok=8ae182&media=2_4_0%3Afeature%3Aarchiveexternalkey.png)*As you can see the link is inactive, you can't open the caller details.*

   In the history of other objects to which they are or were linked, you just get the id of that archived object:![img](https://www.itophub.io/wiki/media?w=600&tok=0ae1d0&media=2_4_0%3Afeature%3Aarchivehistoryexternalkey.png)

   If you try to open the details of that archived object using a bookmarked url or building the url like this: http://myitop/pages/UI.php?operation=details&class=Person&id=11&

   Then you will get a message like this one:

   ![Archived object not visible](https://www.itophub.io/wiki/media?w=800&tok=ad1552&media=2_4_0%3Afeature%3Aarchivedobjectinnormalmode.png)

   When an object is archived, all its n:n linkages to other objects are `archived` as well, meaning that they aren't visible anymore

   ### in Archive mode

   Any user can toggle the archive mode:![Activate archive mode](https://www.itophub.io/wiki/media?w=200&tok=62c541&media=2_4_0%3Afeature%3Aarchivetogglemenu.png)

   - In archived mode, you have a orange tag to remind you that you have activated it.
   - All objects are **read-only**
   - Archived objects are **visible** and tagged as `archived`

   ![Archived object visible](https://www.itophub.io/wiki/media?w=500&tok=d2f647&media=2_4_0%3Afeature%3Aarchivedobjectinarchivemode.png)

   - An attribute referencing an `archived` object is clickable:

   ![External Key to an archived object in archived mode](https://www.itophub.io/wiki/media?w=300&tok=97bf2e&media=2_4_0%3Afeature%3Aarchiveexternalkeyinarchivemode.png)

   If you `desactivate archive mode` while you are on an archived object:![img](https://www.itophub.io/wiki/media?w=200&tok=1278f3&media=2_4_0%3Afeature%3Aarchivetogglemenudesactivate.png)

   you get again the feedback message

   ![Archived object not visible](https://www.itophub.io/wiki/media?w=800&tok=ad1552&media=2_4_0%3Afeature%3Aarchivedobjectinnormalmode.png)