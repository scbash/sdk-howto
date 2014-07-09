# Dealing With Third Party Code in Git

I've often been asked how to integrate blocks of third-party code into a project
(e.g. SDKs, Drupal files, libraries, etc.) in a way that makes updating the
third party code easy.  Having just had to integrate a new SDK into our main
repository at $dayjob, I thought I'd build an example repository to demonstrate
the concept.

The basic process is:
 1. Unpack the third party code into your repo
 2. Commit the third party code as is (even if it's multiple directories)
 3. Modify the code as necessary (e.g. moving files, applying patches, etc.),
    generating one or more commits.
 4. When the third party code requires an update, create a new branch from the
    original commit from step 2.
 5. Remove all the original files and unpack the new ones
 6. Create a new commit.
 7. Switch back to your main branch and merge the new branch.

Git's merge machinery will attempt to integrate all the changes in the third
party code with your local changes, flagging conflicts as necessary.

## This Example

This repository is a tiny instance of the process described above:
 1. I created a new repository
 2. I created three directories, each containing a single file (each file filled
    with text from http://www.lipsum.com/), and committed the files (the
    "initial version" of the "SDK")
 3. I then moved the files into one directory and made minor modifications to
    one of them (this is actually a couple of commits)
 4. I then branched from the initial commit (creating sdk-v2), completely
    replaced bar.txt with new text (to foil any content matching Git might do
    during rename detection), and made a minor (non-conflicting) modifiction to
    baz.c
 5. Switching back to master, I was able to merge sdk-v2 and Git correctly
    integrated the SDK changes with my local reorganization and modifications.

Feel free to clone this repository and explore its history to understand this
process.

