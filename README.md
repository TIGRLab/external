A project for organizing our dbGAP data

### Datasets

- `FHS/` 

  Framingham Cohort

  http://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000007.v25.p9

  Datasets: 41896, 41904

- `CARDIA/` 

  Coronary Artery Risk Development in Young Adults (CARDIA) Study Cohort

  http://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000285.v3.p2

  Datasets:  43161, 43162

- `ADGC/` 

  Alzheimer's Disease Genetics Consortium (ADGC) Genome Wide Association Study
  -NIA Alzheimer's Disease Centers Cohort

  http://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000372.v1.p1

  Datasets: 44719

- `GenADA/`

  Multi-Site Collaborative Study for Genotype-Phenotype Associations in
  Alzheimer's disease and Longitudinal follow-up of Genotype-Phenotype
  Associations in Alzheimer's disease and Neuroimaging component of
  Genotype-Phenotype Associations in Alzheimer's disease 

  http://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000219.v1.p1

  Datasets: 44717, 44718

- `IMSGC/`

  International Multiple Sclerosis Genomics Consortium (IMSGC) Genome Wide Association Study of Multiple Sclerosis 

  http://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000139.v1.p1

  Datasets: 44983, 44984, 44985
  
- `GeneMSA/`

  A Case-Controlled Study for Genotype-Phenotype Associations in Multiple Sclerosis (MS) 

  http://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000171.v1.p1

  Datasets: 44986

### instructions for decrypting dbGaP data

1. Download latest version of [decrypt tools](http://www.ncbi.nlm.nih.gov/Traces/sra/?view=software).  As of Jan 9 2015,
   the version is 2.4.3 (download file = decryption.2.4.3-ubuntu64.tar.gz)

2. Untar: 

        tar -xvf decryption.2.4.3-ubuntu64.tar.gz

3. Run `sratoolkit.jar`, found within `decryption.2.4.3-ubuntu64/bin`:

        java -jar decryption.2.4.3-ubuntu64/bin/sratoolkit.jar

4. In the dialogue box that appears, enter a directory path ending with `ncbi/public`. You will be asked if this
   directory should be created, click yes.

5. Once the "workspace" has been created, select new from the dropdown menu and select "import repository". Browse to
   find the .ngc file that you download from the NIH/dbGaP "Downloads" page for that particular dataset. The .ngc file
   (the "repository key") is the same for each dataset downaloaded as part of the same dbGaP project number (i.e.
   3457).

6. Quit the SRA toolit setup GUI

7. The toolkit setup GUI will have created a file in your home directory (even if you did not specify it as your desired
   respository location) called `~/.ncbi` (hidden). Inside there should be two files, one called `dbGaP-3457.enc_key` (the
   number 3457 here is just an example of a dbGaP project number - this file, created automatically by the SRA toolkit
   setup GUI, should automatically have the correct project number in its name, as it is generated based on the imported
   repository key that includes this information), and one called `user_settings.mkfg`.

8. The `dbGaP-3457.enc_key` file will have the NIH login password in it. It may be out of date, as this password will be
   whichever was used to create the dbGaP project request in the first place (i.e. when the project, not the request for
   any specific dataset within it, was initiated).

9. From anywhere, run the `vdb-passwd` command within `decryption.2.4.3-ubuntu64/bin`. You will be prompted to enter a
   password; enter the original dbGaP password (i.e. the one in the `dbGaP-3457.enc_key` file). You will be prompted to
   re-enter the password; re-enter the same original password. You may encounter a warning saying that a folder (e.g.
   `~/Downloads`) has excessive permissions. Ignore this warning.

10. From the directory containing the ncbi folder (that was created in the first part of step 4), run the `vdb-decrypt`
    command found in `decryption.2.4.3-ubuntu64/bin`, with the top-level folder of the dowloaded data (should be a 5-digit
    number; 41904 is the example below) as the single input.

        decryption.2.4.3-ubuntu64/bin/vdb-decrypt /some_dir/dataset1/41904

11. Throw a pinch of salt over your left shoulder, tap your desk, and cross your fingers.
