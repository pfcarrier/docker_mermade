# Intent

Sharing a way to get up and running quickly with mermade through containerization.

Mermade :
* http://korflab.ucdavis.edu/Datasets/BindNSeq

# Quick startup
Install docker, then run the following :
  ```
  $ ./build
  $ ./run # open a terminal in the container with your PWD mounted in /work
  $ run_mermade.pl # should output the syntax
  ```

If you are using docker-for-windows try the following instead to download the
already build image and run it:
  ```
  $ docker run -v c:\full_path_to_your_fastq_file:/work -it pfcarrier/docker_mermade bash
  ```

> In the command above "c:\full_path_to_your_fastq_file" is usually replaced with
> the directory on your laptop that contain your sequence ( E.g. xxxxx.fastq) file.
>
> Note that the fastq file need to be uncompressed, mermade cannot coop
> with .gz ; the directory should also contain the barcode.txt and background.txt
> file.
>
> When you are inside the container the /work/ directory you are starting in
> is a mount point to c:\full_path_to_your_fastq_file.  This allow mermade to
> access any file that is there.  When inside the container You can run the "ls"
> command to confirm that ; you should see the file it contain listed in the 
> output.

# How to run mermade with your data
Place the following in the same directory as this README.md file :
* background.txt
* barcode.csv
* sequencefile.fastq.gz

Then run the following within the container work directory. E.g.
  ```
  $ rm -rf mermade_output.db wdir
  $ run_mermade.pl -o mermade_output.db -d wdir -b background.txt PRO1071_S1_libDNA_raw_NoIndex_L001_R1.fastq barcode.csv

  # Using test file provided as example
  $ rm -rf mermade_output.db wdir
  $ run_mermade.pl -o mermade_output.db -d wdir -b background.txt BnS13.fastq BnS13-barcodes.csv
  ```

# How to generate a report
From within the container run
  ```
  $ reporter.pl mermade_output.db 5 report_output_1 AAA AAC AAG AAT ACA
  ^^ if you run again change report_output_1 for report_output_2 and so on
  ```

You can then view the generated reports by open the following with your browser,
within the directory where this README.md file is
* report_output_1/index.html

# Test data to play with mermade
* http://korflab.ucdavis.edu/Datasets/BindNSeq/
* You will need :
* http://korflab.ucdavis.edu/Datasets/BindNSeq/background.txt.gz
* http://korflab.ucdavis.edu/Datasets/BindNSeq/BnS13-barcodes.csv
* http://korflab.ucdavis.edu/Datasets/BindNSeq/BnS13.fastq.gz

# Is there a docker hub automated build images ?
Yes
* https://hub.docker.com/r/pfcarrier/docker_mermade/
