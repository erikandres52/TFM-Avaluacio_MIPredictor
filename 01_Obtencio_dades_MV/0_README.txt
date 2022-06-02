1. e2-highmem-16-128
2. wget https://repo.anaconda.com/archive/Anaconda3-2021.11-Linux-x86_64.sh
3. bash Anaconda3-2021.11-Linux-x86_64.sh
4. (reset connection)
5. (Si cal) sudo apt-get update
6. wget --output-document sratoolkit.tar.gz http://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-ubuntu64.tar.gz
7. tar -vxzf sratoolkit.tar.gz
8. export PATH=$PATH:$PWD/sratoolkit.2.11.2-ubuntu64/bin
9. vdb-config -i
10. (Main, enable "Remote access"; Cache, enable "local file-caching", set "Location of user-repository" with name "sratoolkit"; Cloud provider, enable "report cloud instance identifty" of GCP; Exit & Save)
11. wget http://ftp.gnu.org/gnu/parallel/parallel-latest.tar.bz2
12. sudo apt install bzip2
13. tar -xvjf parallel-latest.tar.bz2
14. cd parallel-20220222
15. sudo apt install make
16. sudo ./configure && make
17. cd
18. sudo apt update; sudo apt install parallel; parallel
19. (CTRL-D)
20. sudo apt install samtools
21. sudo apt install python3-pip
22. conda install -c bioconda parallel-fastq-dump
23. conda install -c bioconda kraken2 
24. conda config --prepend channels bioconda
25. conda config --prepend channels conda-forge
26. conda update kraken2
27. vi anaconda3/pkgs/kraken2-2.1.2-pl5262h7d875b9_0/libexec/rsync_from_ncbi.pl
28. (dG)
29. (copy-paste) "rsync_from_ncbi.txt")
30. (:wq)
31. sudo apt install gcc
32. sudo apt install g++
33. sudo apt install unzip
34. kraken2-build --standard --threads 14 --db kraken2/db
35. wget https://github.com/jenniferlu717/Bracken/archive/refs/heads/master.zip
36. unzip Bracken-master.zip
37. bash Bracken-master/install_bracken.sh
38. cp Bracken-master/bracken sratoolkit.2.11.2-ubuntu64/bin/bracken
39. cp Bracken-master/bracken-build sratoolkit.2.11.2-ubuntu64/bin/bracken-build
40. cp Bracken-master/src sratoolkit.2.11.2-ubuntu64/bin/src -r
41. bracken-build -d kraken2/db -t 14 -k 35 -x anaconda3/pkgs/kraken2-2.1.2-pl5262h7d875b9_0/bin
42. pip install humann --no-binary :all:
43b. pip install numpy --upgrade
44. pip install metaphlan
45. mkdir humann3
46. humann_databases --download chocophlan full humann3
47. humann_databases --download uniref uniref90_diamond humann3
48. humann_databases --download utility_mapping full humann3
49. pip install --upgrade daal
50. pip install --upgrade numpy
51. (check metaphlan, bowtie2, diamond)
52. mkdir kraken2/out
53. mkdir humann3/out
54. touch main.sh
55. sudo nano main.sh
56. (copy-paste main.txt)
57. chmod +x main.sh
58. tmux
59. bash main.sh SRA_XXXXXX.txt
60. (cntrl+b then d)
61. tmux attach para comprobar
62. sudo apt install zip
63. (cancel restart)
64. zip -9 -r results.zip kraken2/out humann3/out
65. nano Bracken-master/analysis_scripts/combine_bracken_outputs.py
66 (modificar linia 133 per: taxid = list(sample_counts[name].keys())[0])
67. python Bracken-master/analysis_scripts/combine_bracken_outputs.py --files kraken2/out/*_bracken_S -o merged_bracken_S.txt
68. python Bracken-master/analysis_scripts/combine_bracken_outputs.py --files kraken2/out/*_bracken_S1 -o merged_bracken_S1.txt
69. humann_join_tables --i humann3/out -o merged_genefamilies.tsv --file_name genefamilies
70. humann_join_tables --i humann3/out -o merged_pathabundance.tsv --file_name pathabundance
71. humann_join_tables --i humann3/out -o merged_pathcoverage.tsv --file_name pathcoverage
72. humann_renorm_table -i merged_genefamilies.tsv -o merged_cpm_genefamilies.tsv
73. humann_renorm_table -i merged_pathabundance.tsv -o merged_cpm_pathabundance.tsv
74. humann_renorm_table -i merged_pathcoverage.tsv -o merged_cpm_pathcoverage.tsv
75. (exportar localment tots els arxius merged_X.




