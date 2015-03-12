# mne_utils ####################################################################

Utilities for running MNE in the Winawer Lab using the MEG/EEG setup at NYU.

## Authors #####################################################################

  * Noah C. Benson <[nben@nyu.edu](mailto:nben@nyu.edu)>

## Installation ################################################################

#### Dependencies

All of the scripts included in this repository are python scripts, so python
version 2.7.6 is all that is required. These scripts expect that python is
installed and is on your path, so if you do not have python on your path, you
will need to make sure that it is placed there in your shell initialization
script.

Additionally, you will need to install MNE on your machine. For information on
obtaining and installing MNE, please see the 
[Winawer Lab wiki page](https://wikis.nyu.edu/display/winawerlab/MNE+Setup)
on this topic.

#### Scripts/Path

The mne_utils package includes a directory, bin, which contains all of the
package's scripts.  To use these scripts, you should clone this repository
on your desktop then either call the scripts directory (e.g., 
"~/git/mne_utils/bin/mne_fix_raw") or place this directory on your path, ideally
in your .bashrc or .bash_profile file (assumign you use bash or sh).

## Usage #######################################################################

This package contains the following list of utilities for analyzing MNE data.
Further documentation is available on the
[Winawer Lab wiki pages about using MNE](https://wikis.nyu.edu/display/winawerlab/Using+MNE).

  * **mne_fix_raw**: this script will accepts a directory or gzipped tarball of
    a directory containing the following list of files, processes these files to
    fix the digital trigger channels by converting them into a 
    single integer-valued trigger channel (which is always channel 160 or 161
    for 0- or 1-based indexing, respectively), and converts them into a fiff
    file that can be read by MNE. For more information on how to gather and
    prepare these files, please see the [Winawer Lab wiki page on running MEG
    and EEG experiments for use with MNE](https://wikis.nyu.edu/pages/viewpage.action?pageId=66787871).

    * data_raw.txt: The raw experimental data from the experiment, exported in
      text form from MEG160.
    * marker_coils.elp: The marker coils file.
    * marker_coregistration.hpi: The marker coregistration file.
    * head_shape.hsp: The head shape file.
    * sensor_positions.txt: The sensor positions file.

    These files are required; they do not need to be named exactly as listed
    above, but if the names of these files differ, you will need to specify
    this on the command line; for information on this, run "mne_fix_raw -h".
    Additionally, the following options may be given to mne_fix_raw:

    * -o <filename> or --out <filename> specifies that the resulting fiff file
      should be written to the location given by <filename>; by default this is
      data_raw.fif
    * -q or --quiet specifies that normal messages should be suppressed and only
      warnings and errors should be printed
    * -Q or --quiet-all specifies that only errors should be printed (even
      warnings are suppressed)
    * -v or --verbose specifies that additional debugging messages should be
      printed.
    * -x or --no-mne specifies that instead of running MNE to create the fif
      file then cleaning up the temporary files created, instead, the script
      should create all temporary files then print (to stdout, regardless of
      the level of verbosity specified on the command line) the command that
      would be executed to create the fif file. This is useful if you need to
      perform additional processing after fixing the digital trigger channel but
      before creating the fif file. Note that you are responsible for cleaning
      up the temporary files in this case (they are placed in a temporary
      directory so should be cleaned up by the OS on occasion).
    * -O or --stdout <file> specifies that <file> should be opened and written
      to for all messages or debugging statements instead of printing to
      standard out. Note that if -x is also specified, this file is used instead
      of stdout for printing the command line.
    * -E or --stderr <file> specifies that <file> should be opened and written
      to for all warnings or errors instead of printing to stderr.
      

