# TaxCollector 2.0

[Austin G. Davis-Richardson](mailto:harekrishna@gmail.com)  

---

For the original TaxCollector ([publication](http://www.mdpi.com/1424-2818/2/7/1015/)), please
check out the ["publication" branch](http://github.com/audy/taxcollector/tree/publication).

## About

TaxCollector is a tool for modifying the Ribosomal Database Project (RDP) 16S rRNA database. The RDP database is a fasta file with 16S rRNA sequences. The headers are terribly non-descriptive. Using the NCBI names and nodes databases, this script can create detailed taxonomic descriptions.

For example, this script takes the default RDP header:

    >S001018666 uncultured Acidobacteria bacterium; 2YMLF03; EF630306

And converts it to this:
    [1]Bacteria;[2]Acidobacteria;[3]Acidobacteria_(class);[4]Acidobacteriales;[5]Acidobacteriaceae;[6]"uncultured_Acidobacteriaceae";[7]uncultured_Acidobacteriaceae;[8]uncultured_Acidobacteriaceae_bacterium

This can be useful for some people. For others, not.

## Invocation

### TaxCollector

Otherwise, invoke _comme ca_

    python taxcollector.py names.dmp nodes.dmp input.fasta > output.fasta

You can get names.dmp and nodes.dmp from [NCBI's FTP site](ftp://ftp.ncbi.nih.gov/taxdump.tar.gz).

My favorite way to do this is by typing

    curl ftp://ftp.ncbi.nih.gov/pub/taxonomy/taxdump.tar.gz | gunzip | tar -xvf names.dmp nodes.dmp

The FASTA file must come from RDP [http://rdp.cme.msu.edu].


### Removing unwanted records

There is a script included to remove duplicate records (records that have exactly the same sequence), as well as records that contain the following words in the header (before taxcollecting):

	eukarya, clone, plasmid, cloning_vector, chloroplast
	
	(case in-sensitive)

	Usage:

	`python filter_and_remove_duplicates.py rdp.fa > rdp_filtered.fa`

### Rakefile

For simplicity, there is a Rakefile that retrieves all required databases from their sources, filters duplicates and unwanted "words", and creates the TaxCollector database.

Just cd into the `taxcollector/` directory and type `rake`. This will result in creation of the file: `tc_rdp.fa`, which is your TaxCollector database.

## License

This software is distributed under the [GNU GPL 2.0 software license](http://www.gnu.org/licenses/gpl.html).

Please Cite: Giongo A., Davis-Richardson A.G., Crabb D.B., Triplett E.W. TaxCollector: Modifying Current 16S rRNA Databases for the Rapid Classification at Six Taxonomic Levels. *Diversity*. __2010__; 2(7):1015-1025.