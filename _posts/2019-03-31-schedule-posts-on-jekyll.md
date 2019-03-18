# How to schedule blog posts when using Jekyll and Github

1. Add this line to _config.yml

        future: false
    
    This changes causes Jekyll to ignore any posts with dates in the future

2. Create a post with the desired posting date

    2019-03-31-schedule-posts-on-jekyll.md
    
3. Schedule a task to force Gitgub to rebuild your site every night

    Use your favorite scheduler running from another xomputer to execute this task every night at your chosen time:

This article is based on the excellent instructions I found here: https://shot511.github.io/2018-12-03-how-to-schedule-posts-with-jekyll/
Please refer to that article if you need more details about how to set up the scheduler task.

This article was posted using the same scheduling solution. It works! :)

Thanks for reading.
--fnds
