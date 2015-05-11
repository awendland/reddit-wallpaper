reddit-wallpaper*
=================

Download pictures from from various subreddits ([Reddit](https://reddit.com)) to be cycled through as desktop wallpapers.

* This program is heavily based off of [reddit-background](https://github.com/rconradharris/reddit-background) by [@rconradharris](https://github.com/rconradharris).

![Screenshot](screenshot.jpg?raw=true)

Features
--------

- Integrates with OS folder-based background rotation
- Handles multiple subreddits
- Image resolution filtering ensures your backgrounds are always beautiful
- Flexible sorting lets you choose the quality of images it downloads

Try It
------

1.  Download the project; or clone the repo using [git](http://git-scm.com/), like:

        git clone https://github.com/awendland/reddit-wallpaper.git

2.  Run it:

        cd reddit-wallpaper
        ./reddit-wallpaper

3.  reddit-wallpaper will download the last week's top voted images with a minimum resolution of 1024x768 (though most are higher red), to `~/reddit-wallpaper`.

4.  You can now set your desktop wallpaper to cycle through the images in this folder

    * For OSX: [About.com: Personalize Your Mac's Desktop Wallpaper](http://macs.about.com/od/switchersnewusers/qt/wallpaper.htm)
    * For Windows: [Microsoft.com: Create a desktop background slide show](http://windows.microsoft.com/en-us/windows7/create-a-desktop-background-slide-show)

The default is to use images from [/r/CityPorn](https://reddit.com/r/CityPorn).

Install It
----------

The easiest way to install reddit-wallpaper is to copy it to
`/usr/local/bin`. To do this, run this command:

    cp reddit-wallpaper /usr/local/bin

Now you can run `./reddit-wallpaper` whenever you would like to update the batch of images, or you can [automate it](#automate-it).

Configure It
------------

If you'd like to customize reddit-background so that it chooses images images from different subreddits, you can provide a configuration file at `~/.reddit-wallpaper.conf`. Here’s a sample to get you started:

    # Default is used across all monitors, unless overriden with a more
    # specific configuration
    [default]

    # CityPorn has gorgeous cityscape photos, and BeachPorn has enviable beach/sand/wave photos
    subreddits=CityPorn,BeachPorn

    # Filter out any images with resolution below this
    min_resolution=1280x1024

    # Directory in which to download images
    download_dir=~/reddit-wallpaper

Automate It
-----------

Once you have a configuration you like, you can set up reddit-wallpaper to query for new images weekly.

There are a number of ways to do this, but one way is to add it to your *crontab*.

To do this, open up your crontab in an editor:

    crontab -e

And once you’ve done that, add the following line:

    0 0 * * 0 /usr/local/bin/reddit-wallpaper

Save the file and quit the editor. Now your wallpaper stash will update weekly at 12:00 am on Sunday. The update will download new images from the subreddits and remove any old images from the download directory.

Advanced
--------

### Subreddit Sort Options

By default, when you specify a subreddit, you are selecting the top 25 posts over the last week.

You can customize the sort by using the following format:

    <subreddit>:[sort]:[limit]:[timeframe]

| Argument  | Possible Values                                        | Default |
|-----------|--------------------------------------------------------|---------|
| subreddit | A subreddit                                            | *None*  |
| sort      | controversial, gilded, hot, new, promoted, rising, top | top     |
| limit     | An integer                                             | 25      |
| timeframe | all, day, hour, month, week, year                      | week    |

So, for example, if you want to only include the 5 newest posts from [/r/EarthPorn](https://reddit.com/r/EarthPorn), you would write it as:

    EarthPorn:new:5

Or if you’d like to include the top 10 posts over the year for [/r/CityPorn](https://reddit.com/r/CityPorn), you’d write it as:

    CityPorn:top:10:year

**NOTE:** Only the `top` and `controversial` sort methods use the `timeframe` option.

### Command-Line Usage

In addition to specifying a configuration file, you can also customize reddit-wallpaper directly from the command-line.

The arguments represent each subreddit you would like to pull images from. For example, to pull city images and images from [/r/CarPorn](https://reddit.com/r/CarPorn), you would run:

    reddit-wallpaper CityPorn CarPorn

If you want to clear all currently downloaded images and redownload everything you would run:

    reddit-wallpaper --clear

You can stipulate where to download the images to by using:

    reddit-wallpaper --download-dir "~/some-other-directory"

If you'd like to adjust the minimum resolution of the images:

    reddit-wallpaper --min-resolution 1920x1080

### Attribution and License

This program is heavily based off of the work done by [@rconradharris](https://github.com/rconradharris) for [reddit-background](https://github.com/rconradharris/reddit-background). This program was created because the desired use case was not covered by reddit-background, particularly that the background could only be changed for one of the user's spaces. Furthermore, OSX has a built in mechanism for rotating through wallpaper images in a folder, so this program was created to integrate with that existing OS functionality.

This program is licensed under the MIT License, which can be viewed at [LICENSE.txt](LICENSE.txt?raw=true).