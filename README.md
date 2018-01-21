# Intent

Sharing a way to get up and running quickly with mermade through containerization.

Mermade :
* http://korflab.ucdavis.edu/Datasets/BindNSeq

# Quick startup
Install docker, then run the following :
  ```
  ./build
  ./run # open a terminal in the container with your PWD mounted in /work
  run_mermade.pl # should output the syntax
  ```

# How to run mermade with your data
Place the following in the same directory as this README.md file :
* background.txt
* barcode.csv
* sequencefile.fastq.gz

Then run the following within the container work directory. E.g.
  ```
  rm -rf mermade_output.db wdir
  run_mermade.pl -o mermade_output.db -d wdir -b background.txt PRO1071_S1_libDNA_raw_NoIndex_L001_R1.fastq barcode.csv

  # Using test file provided as example
  rm -rf mermade_output.db wdir
  run_mermade.pl -o mermade_output.db -d wdir -b background.txt BnS13.fastq BnS13-barcodes.csv
  ```

# How to generate a report
From within the container run
  ```
  reporter.pl mermade_output.db 5 report_output_1 AAA AAC AAG AAT ACA
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
