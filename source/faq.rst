.. _faq:

%%%%%%%%%%%
Kurento FAQ
%%%%%%%%%%%

This is a list of Frequently Asked Questions about Kurento.  Feel free to
suggest new entries or different wording for answers!

How do I...
-----------

...know how many :rom:cls:`pipelines<MediaPipeline>` do I need for my Application?
    :rom:cls:`Media elements<MediaElement>` can only communicate
    with each other when they are part of the same pipeline.
    Different MediaPipelines in the server are independent do not share
    audio, video, data or events.

    .. todo:: Endpoints???

        How many Endpoints are needed in a given pipeline?

    A good heuristic is that you will need one pipeline per each
    set of communicating partners in a channel, and one Endpoint in
    this pipeline per audio/video streams reaching a partner.


...know to what client a given WebRtcEndPoint belongs or where is it coming from?
    Kurento API currently offers no way to get application attributes
    stored in a :rom:cls:`MediaElement`. However, the application developer
    can maintain a hashmap or equivalent data structure mapping
    the :rom:cls:`WebRtcEndpoint`  internal Id (which is a string) to
    whatever application information is desired.

...stop kurento installing nvidia drivers in my machine?
    Kurento uses libopencv-dev to get auxiliary files for several
    Computer Vision algorythms in its filters. This package is part
    of the :wikipedia:`Open Source Computer Vision Library<en,OpenCV>`.

    libopencv-dev depends on libopencv-ocl-dev, which depends on
    libopencv-ocl2.4 which depends on virtual <libopencl1>, provided
    by any of
        * ocl-icd-libopencl1
        * nvidia-304
        * nvidia-304-updates
        * nvidia-319
        * nvidia-319-updates

    Further, ocl-icd-libopencl1 conflicts with all the nvidia-* packages.
    As the Ubuntu 13.10, when none of those packages are installed,
    the package manager chooses nvidia-319-updates, which breaks OpenGL
    acceleration for Intel graphics cards. To check for the problem,
    if you install kurento or need to install libopencv-dev on a Intel
    graphics computer, please do:

    .. sourcecode:: console

        $ dpkg-query -l nvidia*
        Desired=Unknown/Install/Remove/Purge/Hold
        | Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
        |/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
        ||/ Name                              Version           Architecture        Description
        +++-=================================-================-=============-==========================
        un  nvidia-304                        <none>                         (no description available)
        un  nvidia-304-updates                <none>                         (no description available)
        un  nvidia-319                        <none>                         (no description available)
        un  nvidia-319-updates                <none>                         (no description available)
        ii  ocl-icd-libopencl1:amd64          2.0.2-1ubuntu1   amd64         Generic OpenCL ICD Loader
        $ # if you have any of those five packages installed, all chances are that all will be ok
        $ # if you have neither, you should probably be installing ocl-icd-libopencl1 like:
        $ sudo apt-get install ocl-icd-libopencl1


Why can't I...
-----------

...install the kurento media server with an Ubuntu LTS version?
    If you read this message after April 2014, odds are that you will be able
    to use one, as `trusty tahr <http://cdimage.ubuntu.com/releases/14.04/>`__
    is in the beta stage as this entry is written. See `the calendar for LTS
    versions <https://wiki.ubuntu.com/LTS>`__.

    The reason why kurento is using Ubuntu 13.10 is that it uses `gstreamer
    1.0 <https://launchpad.net/ubuntu/saucy/amd64/libgstreamer1.0-dev>`__,
    which 13.10 keeps at the 1.2 version. While we are providing `a ppa
    <https://launchpad.net/~kurento/+archive/kurento>`__ with the packages,
    building those against older releases is a difficult task without
    updating lots of packages. You can also build from sources 