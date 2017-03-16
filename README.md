# redditfs

Everything is better in an 80x25 green-and-black terminal -- even Reddit! `redditfs` maps subreddits to a FUSE filesystem, so you can use your favorite shell (or GUI file browser, or SSH, or FTP) to browse Reddit.

## Example

    $ ls -l /r/programming
    total 0
    dr-xr-xr-x@ 3 root  wheel  0 Jan 16 10:30 ANN:_pandas_0130_released
    dr-xr-xr-x@ 3 root  wheel  0 Jan 18 13:08 An_evaluation_of_simple_Python_performance_tweaks
    dr-xr-xr-x@ 3 root  wheel  0 Jan 17 08:36 Anyone_have_experience_installing_Folium_for_Py_33?
    dr-xr-xr-x@ 3 root  wheel  0 Jan 18 09:48 Are_there_any_python_made_games_on_Steam?
    dr-xr-xr-x@ 3 root  wheel  0 Jan 16 20:06 Beginner:_Getting_Beyond_Syntax
    dr-xr-xr-x@ 3 root  wheel  0 Jan 18 00:53 Best_Questions_to_ask_when_hiring_a_Python_dev?
    ...
    $ ls -l /r/programming/An_evaluation_of_simple_Python_performance_tweaks
    total 16
    -r--r--r--@ 1 root  wheel  97 Jan 18 13:08 permalink
    -r--r--r--@ 1 root  wheel   0 Jan 18 13:08 selftext
    -r--r--r--@ 1 root  wheel  72 Jan 18 13:08 url
    $ cat /r/programming/Best_Questions_to_ask_when_hiring_a_Python_dev?/selftext
    I'm a long time C/C++/C# dev who is now diving into python head on, and using it
     on a project here in Seattle.  Part of this is I need to grow my team and hire 
    ...
    $ lynx $(cat /r/programming/An_evaluation_of_simple_Python_performance_tweaks/url)
    
## Howto

You'll need Python >= 2.7 or >= 3.4, and FUSE. You can install FUSE via the package managers on most Linux distros. On OSX, you can get FUSE support via [OSXFUSE](http://osxfuse.github.io/).

    $ git clone https://github.com/ianpreston/redditfs.git
    $ cd redditfs && virtualenv env && source env/bin/activate
    $ pip install -r reqs.txt
    $ mkdir /r
    $ python redditfs.py /r

## Windows Howto

You'll need Python >= 2.7 or >= 3.4, and [WinFsp](https://github.com/billziss-gh/winfsp/releases). You also need [fusepy](https://github.com/billziss-gh/fusepy).

    C:\...\redditfs>set PYTHONPATH=path\to\fusepy

    C:\...\redditfs>python redditfs.py R:
    The service python has been started.

Then from a different prompt:

    C:\...>dir R:\programming\*
     Volume in drive R has no label.
     Volume Serial Number is D9C7-94B3

     Directory of R:\programming

    03/16/2017  02:37 PM    <DIR>          .
    03/16/2017  02:32 PM    <DIR>          ..
    03/16/2017  07:49 AM    <DIR>          a_case_for_fixmes_in_production_code
    03/16/2017  03:32 AM    <DIR>          a_type-safe_typescript_immutable_library
    03/16/2017  01:24 PM    <DIR>          acing_the_technical_interview
    03/16/2017  12:18 PM    <DIR>          an_upgrade_to_syntaxnet,_new_models_and_a_parsing_competition
    03/16/2017  11:14 AM    <DIR>          announcing_guetzli_a_new_open_source_jpeg_encoder_[by_google]
    03/16/2017  10:31 AM    <DIR>          announcing_rust_1.16
    03/15/2017  06:18 PM    <DIR>          beautiful_racket
    03/16/2017  11:44 AM    <DIR>          client-server_web_games_with_webrtc
    03/16/2017  04:33 AM    <DIR>          error_handling_exception_or_result
    03/15/2017  10:38 AM    <DIR>          gitter_+_gitlab_=_win
    03/16/2017  07:13 AM    <DIR>          gnu_guile_2.2.0_released
    03/16/2017  05:23 AM    <DIR>          keeping_python_projects_secure_on_gitlab
    03/16/2017  06:54 AM    <DIR>          opus_-_open_source_knowledge_base_application_for_teams
    03/15/2017  02:11 AM    <DIR>          overclocking_tools_for_nvidia_gpus_suck,_i_made_my_own.
    03/16/2017  03:38 AM    <DIR>          practical_color_theory_for_people_who_code
    03/16/2017  02:18 PM    <DIR>          redshift_pitfalls_and_how_to_avoid_them
    03/16/2017  08:58 AM    <DIR>          tail_recursion,_do_i_have_it_how_to_get_it
    03/15/2017  09:50 PM    <DIR>          the_eigenvector_of_why_we_moved_from_language_x_to_language_y
    03/16/2017  10:12 AM    <DIR>          web_scraping_bypassing_“403_forbidden,”_captchas,_and_more
    03/16/2017  03:13 AM    <DIR>          why_i_love_programming
    03/16/2017  09:50 AM    <DIR>          why_qt_and_not_imgui
    03/16/2017  12:23 PM    <DIR>          windowise_wisely_create_windowmodalnotificationpush_in_webpages._promise-based.
    03/15/2017  04:24 PM    <DIR>          winfsp_2017_–_fuse_for_windows_–_is_finally_here
    03/16/2017  06:39 AM    <DIR>          wolfenstein_3d_controlled_by_sound
                   0 File(s)              0 bytes
                  26 Dir(s)               0 bytes free

    C:\...>type R:\programming\winfsp_2017_–_fuse_for_windows_–_is_finally_here\url
    http://www.secfs.net/winfsp/blog/files/winfsp-2017.html

## License

Available under the MIT License.
