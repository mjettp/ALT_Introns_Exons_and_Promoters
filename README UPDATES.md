# Telomeres Shorten with Age
Human telomeres are estimated to be 5,000 - 15,000 base pairs at birth (Sanders 2013). The end replication problem shortens telomeres by approximately 50 bp with each round of cell division (Proctor 2002). 

ADD
telomere reduces
48 bp every cell divisions (23)
Hastie, N. D., Dempster, M., Dunlop, M. G., Thompson, A. M.,
Green, D. K., and Allshire, R. C. (1990) Telomere reduction in
human colorectal carcinoma and with aging. Nature 346, 866 –
868.
ADD TELOMERE SHORTENING

ADD SHAY 2016 FIGURE 1 WITH ALT UPDATES

#### Simple 1 Telomere Shortening Model
Here's a simple mathematical model for one telomere:

```python
#!/usr/bin/env python
starting_length = 15000
division_loss = 50
current_length = starting_length
current_division_number = 1
while current_length > 0:
    print "Telomere Length is " + str(current_length) + " bp" + " after " + str(current_division_number) + " divisions."
    current_length = current_length - 50
    current_division_number += 1
print "The telomere is gone!"
```

Here are the last couple of lines of output:

```sh
Telomere Length is 350 bp after 294 divisions.
Telomere Length is 300 bp after 295 divisions.
Telomere Length is 250 bp after 296 divisions.
Telomere Length is 200 bp after 297 divisions.
Telomere Length is 150 bp after 298 divisions.
Telomere Length is 100 bp after 299 divisions.
Telomere Length is 50 bp after 300 divisions.
The telomere is gone!
```

#### Simple 1 Telomere Model & Damage Checkpoint
The situation is more complicated than that model. A DNA damage checkpoint will be triggered aroudn 5k bp and there will be massive genomic instability and cell death at around 3k bp (Harley 2008). Here's that slightly more complicated model:

ADD DATA ON ESCAPING CELL CYCLE CHECKPOINTS HERE
In human cells,
the bypass or escape from senescence can be experimentally
demonstrated by abrogating important cell-cycle checkpoint
genes [such as TP53 (p53), CDKN1A (p21), CDKN2A (p16 INK4a ),
and RB1 (pRb)], leading to increased numbers of cell divisions
of potentially initiated premalignant cells ( 31–34 )
Shay JW , Wright WE . Historical claims and current interpretations
of replicative aging . Nat Biotech 2002 ; 20 : 682 – 8 .
32. Wright WE , Shay JW . The two-stage mechanism controlling cellular
senescence and immortalization . Exp Gerontol 1992 ; 27 ; 383 – 9 .
33. Shay JW , Wright WE , Werbin H . Defi ning the molecular mechanism of
human cell immortalization . Biochim Biophys Acta . 1991 ; 1072 : 1 – 7 .
34. Harley CB. Telomere los
ADD DATA ON ESCAPING CELL CYCLE CHECKPOINTS HERE

ADD SHAY 2016 FIGURE 3 ABOUT ESCAPING SENSESCNECE CHECKPOINTS HERE

```python
#!/usr/bin/env python
starting_length = 15000
division_loss = 50
current_length = starting_length
current_division_number = 1

while current_length > 0:
    if current_length > 5000:
        print "Telomere Length is " + str(current_length) + " bp" + " after " + str(current_division_number) + " divisions."
    elif current_length > 3000:
        print "p53-dependent arrest triggered @ " + str(current_length) + " bp" + " after " + str(current_division_number) + " divisions."
        print "BUT, this cell has transforming mutations! It continues to divide!"
    elif current_length > 0:
        print "Genomic instability is causing new mutations at " + str(current_length) + " bp" + " after " + str(current_division_number) + " divisions."
        print "Death is inevitable, UNLESS telomere length is stabilized!"
    else:
        print "David is a bad programmer, lol"
    current_length = current_length - 50
    current_division_number += 1
print "The telomere is gone!"
```

Here are the last couple of lines of output:

```sh
Genomic instability is causing new mutations at 200 bp after 297 divisions.
Death is inevitable, UNLESS telomere length is stabilized!
Genomic instability is causing new mutations at 150 bp after 298 divisions.
Death is inevitable, UNLESS telomere length is stabilized!
Genomic instability is causing new mutations at 100 bp after 299 divisions.
Death is inevitable, UNLESS telomere length is stabilized!
Genomic instability is causing new mutations at 50 bp after 300 divisions.
Death is inevitable, UNLESS telomere length is stabilized!
The telomere is gone!
```

#### 92 Telomere Shortening Model
There are 92 telomeres / human cell. That's cause there are 23 chromosomes X 2 (paired) X 2 telomeres/chrosome = 92. A DNA damage checkpoint will get triggered by the shortest telomere (Harley 2008). So a better mathematical model would take into account the distribution of telomere lengths and each individual telomere's shortening. NOTE: THE RANGE OF TELOMERE LENGTHS ISN'T NECESSARILY WHAT I HAVE DEPICTED HERE. I NEED TO TAKE SUDA 2002 INTO ACCOUNT IN A FUTURE UPDATE. My intuition is that the range I've used here may be closer to the range of telomere lengths in ALT, but I need to do the math to be sure ... See table 1 of Suda 2002 for the estimated telomere lengths of chromosomes 1-22 for the GM130B cell line. 

GM130B is a spontaneously immortalized lymphoblast line from a male human. It's probably TEL+ because it's of a blood stem cell lineage (I explain this thinking in a later section), but I wasn't able to answer that conclusively. The search phrase of 'GM130B lymphoblast "telomerase"' is problematic cause there is an antibody called GM130 antibody called gm130 https://www.abcam.com/gm130-antibody-ep892y-cis-golgi-marker-ab52649.html. I also tried 'GM130B lymphoblast "telomerase" -antibody', BUT there's a Rab1b and Rab1-binding protein called GM130. So I tried 'GM130B lymphoblast "telomerase" -antibody -golgi' and that didn't have any useful results. 

TAKE THESE OTHER TELOMERIC LENGTH RANGES INTO ACCOUNT
The lengths of (TTAGGG)n tracts have been shown to
vary from telomere to telomere within individual cells
(Lansdorp et al., 1996; Zijlmans et al., 1997; Graakjaer et al.,
2004) and between alleles at the same telomere (Baird et al.,
2003; der-Sarkissian et al., 2004).
Lansdorp PM, Verwoerd NP, van de Rijke FM,
Dragowska V, Little MT, et al: Heterogeneity in
telomere length of human chromosomes. Hum
Mol Genet 5: 685–691 (1996)
Zijlmans JM, Martens UM, Poon SS, Raap AK, Tan-
ke HJ, et al: Telomeres in the mouse have large
inter-chromosomal variations in the number of
T2AG3 repeats. Proc Natl Acad Sci USA 94:
7423–7428 (1997)
Graakjaer J, Pascoe L, Der-Sarkissian H, Thomas G,
Kolvraa S, et al: The relative lengths of individ-
ual telomeres are defined in the zygote and
strictly maintained during life. Aging Cell 3:
97–102 (2004).
Baird DM, Rowson J, Wynford-Thomas D, Kipling
D: Extensive allelic variation and ultrashort
telomeres in senescent human cells. Nat Genet
33: 203–207 (2003).
Der-Sarkissian H, Bacchetti S, Cazes L, Londono-
Vallejo JA: The shortest telomeres drive karyo-
type evolution in transformed cells. Oncogene
23: 1221–1228 (2004).

TAKE THESE OTHER TELOMERIC LENGTH RANGES INTO ACCOUNT

```python
#!/usr/bin/env python
import random
shortest = 5000
longest = 15000
num_of_telomeres = 92
telomeres_longer_than_3000 = True
current_division_number = 1

def initialze_92_telomere_lengths(shortest, longest, num_of_telomeres):
    telomere_length_list = []
    for j in range(num_of_telomeres):
        telomere_length_list.append(random.randint(shortest, longest))
    return telomere_length_list
#print "This is the initial list of telomere lengths: "
initial_list_of_telomere_lengths = initialze_92_telomere_lengths(shortest, longest, num_of_telomeres)
#print(initial_list_of_telomere_lengths)
current_list_of_telomere_lengths = initial_list_of_telomere_lengths

while telomeres_longer_than_3000 == True:
    print "It is division # " + str(current_division_number)
    print "This is the current list of telomere lengths: "
    print current_list_of_telomere_lengths

    current_telomere_number = 1
    for telomere in current_list_of_telomere_lengths:
        if telomere <= 5000 and telomere > 3000:
            print "Telomere number " + str(current_telomere_number) + " is only " + str(telomere) + " bp long."
            print "p53-mediated senescence would be triggered, BUT p53 is mutated!"
        elif telomere <= 3000:
            print "Telomere number " + str(current_telomere_number) + " is only " + str(telomere) + " bp long."
            print "There is massive genomic instability and cell death!"
            telomeres_longer_than_3000 = False
            break
        current_telomere_number += 1

    current_list_of_telomere_lengths = [telomere-50 for telomere in current_list_of_telomere_lengths]
    current_division_number += 1
```

THIS DISAGREES WITH Given the size of the telomere loss at each replication
and the average telomere length at conception, telomer-
ase negative cells have the capacity for about 100 cell
divisions before telomeres get critically short (Harley,
1995)
THIS DISAGREES WITH HARLEY 1995 ... IS 5000 TOO SHORT OF STARTING POINT?
TALK ABOUT DAGG 2017 Start-
ing from a single cell, 40 cell divisions are sufficient to generate
2 40 cells, with a mass of 1 kg. Many types of normal cells are
capable of more than 40 cell divisions, which raises the question
why immortalization is required for oncogenesis.
TALK ABOUT DAGG 2017

Here are the last couple of lines of output:

```sh
It is division # 44
This is the current list of telomere lengths: 
[9767, 10391, 3833, 4927, 8548, 3772, 8590, 6477, 12382, 6371, 11163, 8084, 9051, 6639, 5095, 3255, 9457, 12712, 9600, 4238, 5625, 11407, 12178, 8371, 9155, 2987, 8131, 8252, 4487, 10558, 10815, 5485, 3111, 8113, 8712, 7742, 11029, 8390, 5037, 5735, 9947, 5511, 10571, 11775, 5692, 12405, 3322, 4462, 6719, 11184, 8716, 8806, 11079, 8928, 7915, 10267, 6327, 3418, 6933, 6367, 3025, 10936, 9219, 12174, 3180, 11997, 9131, 7859, 7225, 8068, 10717, 12644, 12291, 3080, 12679, 7654, 3982, 7852, 5535, 10338, 11876, 11217, 5231, 9777, 3649, 6365, 6236, 7214, 7799, 8292, 3725, 7978]
Telomere number 3 is only 3833 bp long.
p53-mediated senescence would be triggered, BUT p53 is mutated!
Telomere number 4 is only 4927 bp long.
p53-mediated senescence would be triggered, BUT p53 is mutated!
Telomere number 6 is only 3772 bp long.
p53-mediated senescence would be triggered, BUT p53 is mutated!
Telomere number 16 is only 3255 bp long.
p53-mediated senescence would be triggered, BUT p53 is mutated!
Telomere number 20 is only 4238 bp long.
p53-mediated senescence would be triggered, BUT p53 is mutated!
Telomere number 26 is only 2987 bp long.
There is massive genomic instability and cell death!
```

It's hard to picture that list of telomere lengths, so I've made a barplot in R. Note that the red line is for the 5 kb p53-mediated senescence and that the black line is the 3 kbp cell crisis point (Harley 2008). Note that the telomere lengths from the Python code don't match the ones I used for the R code. The R code #s are from an earlier attempt. You could use the code from the Telomere_Math_Models folder to replicate this stuff.

```r
telomere_lengths <- list(5583, 12162, 6389, 9970, 10351, 7970, 10257, 10570, 11226, 10003, 12418, 5145, 9841, 8593, 3683, 9251, 7884, 5070, 9813, 5316, 6170, 5067, 6420, 10141, 3465, 6754, 11450, 5883, 11551, 7127, 7170, 11200, 7788, 7079, 5492, 11992, 8606, 11573, 4600, 6108, 9872, 9659, 7811, 8597, 6907, 3161, 5425, 7053, 5638, 5540, 12154, 7962, 11386, 5722, 6675, 11306, 2967, 11208, 10478, 8560, 12603, 7522, 10607, 4044, 6816, 4172, 5127, 8953, 7438, 9860, 11952, 4076, 11505, 8247, 9124, 6027, 12625, 3031, 8991, 4777, 5177, 9458, 5578, 7392, 6019, 4637, 4912, 4458, 11358, 5594, 12343, 3874)
telomere_numbers <- 1:92
typeof(telomere_lengths[1])
test <- barplot(as.numeric(telomere_lengths), main="Telomere Lengths", xlab="Telomere Number", ylab="Telomere Length (bp)", ylim = c(0,15000))
abline(h=5000, col="red", lwd=3)
abline(h=3000, col="black", lwd=3)
```

![Telomere_Shortening_Bar_Graph](/Assets/Telomere_Shortening_Bar_Graph.jpg "Telomere_Shortening_Bar_Graph")

# Telomere Maintenance Mechanism (TMM) Selection
The selection of TMM seems to mainly depend upon telomerase chromatin compaction and mutations in ATRX & p53 (Gocha 2013). 
 
![ALT_TEL_Permissive_Mutations](/Assets/ALT_TEL_Permissive_Mutations.jpg "ALT_TEL_Permissive_Mutations")

(Gocha 2013)

# Telomerase Extends Telomeres
Telomerase adds 5'-GGTTAG-3' (Harley 2008). Telomerase extends the shortest telomeres first (Harley 2008, Cristofari 2006). The G-rich strand is 5'-GGTTAG-3' and the C-rich strand is 3'-CCAATC-5'. Telomerase adds 5'-GGTTAG-3' (Harley 2008). The telomerase enzyme TERT uses the telomerase RNA 3'-CAAUCCCAAUC-5' as a template for the extension (Gavory 2002). There is a G-rich single stranded telomeric overhang of 130-210 nucleotides (Cesare 2010). telomerase, which is a reverse transcriptase that adds repetitive telomeric DNA (TTAGGG)n to the ends of the chromosomes (Allsopp 2001). 

ADD SECTION ABOUT TELOMERASE MUTATIONS!
Somatic mutations in the
proximal promoter of the human telomerase reverse tran-
scriptase gene (TERT ) are now considered the most common
noncoding mutation in cancer.
Bojesen SE , Pooley KA , Johnatty SE , Beesley J , Michailidou K , Tyrer
JP , et al. Multiple independent variants at the TERT locus are asso-
ciated with telomere length and risks of breast and ovarian cancer .
Nat Genet 2013 ; 45 ; 371 – 384 .
38. Heidenreich B , Rachakonda PS , Hemminki K , Kumar R . TERT
promoter mutations in cancer development . Current Opin Genet
Develop 2014 ; 24 : 30 – 7 .
39. Huang FW , Hodis E , Xu MJ , Kryukov GV , Chin L , Garraway LA .
Highly recurrent TERT promoter mutations in human melanoma .
Science 2013 ; 339 : 957 – 9 .
40. Chiba K , Johnson JZ , Vogan JM , Wagner T , Boyle JM , Hockemeyer
D . Cancer-associated TERT promoter mutations abrogate telomer-
ase silencing . eLife 2015 ; 4e07918 .
41. Killela PJ , Reitman ZJ , Jiao Y , Bettegowda C , Agrawal N , Diaz LA Jr ,
et al. TERT promoter mutations occur frequently in gliomas and a
subset of tumors derived from cells with low rates of self-renewal .
Proc Natl Acad Sci U S A 2013 ; 110 : 6021 – 6 .
42. Vinagre J , Almeida A , Pópulo H , Batista R , Lyra J , Pinto V , et al.
Frequency of TERT promoter mutations in human cancers . Nature
Comm 2013 ; 4 : 2185 .
43. Horn S , Figl A , Rachakonda PS , Fischer C , Sucker A , Gast A , et al.
TERT promoter mutations in familial and sporadic melanoma .
Science 2013 ; 339 : 959 – 61 .
44. Stern JL , Theodorescu D , Vogelstein B , Papadopoulos N , Cech
TR . Mutation of the TERT promoter switch to active chromatin,
and monoallelic TERT expression in multiple cancers. Genes Dev
2015 ; 29 : 1 – 6
or alterations in
TERT splicing ( 52 )
Wong MS , Wright WE , Shay JW . Alternative splicing regulation of
telomerase: a new paradigm? Trends Genet 2015 ; 30 ; 10 : 430 – 8 .
SPECIFICLALY ABOUT REF 44 monoallelic TERT promoter mutations
must provide a selective advantage in specifi c tumor types, such
as glioblastomas, urothelial carcinomas, and melanomas, possi-
bly by retaining an active chromatin state ( 44 )
ADD SECTION ABOUT TELOMEASE MUTATIONS!



#### Model of Different Telomerase Levels
Telomerase overexpression might have an upper limit of 0.8 kb/division ... I'm not certain, but that was reported in Cristofari 2006. I might want to create a future update that limits to 800 bases/division just to keep cellular resources in mind. I don't know how model the telomerase activity in Python with a great deal of biological accuracy ... 

1. How much RNA template is available?
2. How long will a telomerase enzyme be active?
3. How do you model 3-D interactions?
etc.,

so I've decided to simplify the telomerase model to the number of times that telomerase can add 6bp of telomere to the chromosome end. Yes, it's a spherical cow kind of model, but what could I do better? Seriously, message me if you've got an idea, cause I'll try it out :) The telomere shortening model from above shortens 50 bp/ telomere for the 92 telomeres, so that's 4600 bp that is lost per division. 4600/6 = 766.6, so 6*676 bp being added per cell division would be cellular immortality. Anything lower-ish will eventually senesce.  This code is mostly the same as the last bit of telomere shortening code. I won't waste space witht he whole code again (see the Telomere_Math_Models folder). All I did was nest this while loop inside the first while loop (the one that shortens the telomeres). 

```python
    telomerase_bp_added_per_division = 0
    telomere_bp_left_to_add = telomerase_bp_added_per_division
    while telomere_bp_left_to_add > 0:
        # get index for shortest telomere
        shortest_telomere_index = current_list_of_telomere_lengths.index(min(current_list_of_telomere_lengths))
        # get length of shortest telomere
        length_of_shortest_telomere = current_list_of_telomere_lengths[shortest_telomere_index]
        # add 6bp to shortest telomere
        new_length_of_shortest_telomere = current_list_of_telomere_lengths[shortest_telomere_index] + 6
        # change list entry at index # to new telomere length
        current_list_of_telomere_lengths[shortest_telomere_index]=new_length_of_shortest_telomere
        # less telomerase left
        telomere_bp_left_to_add = telomere_bp_left_to_add - 6
```

Recall that the default setting of 0 for telomerase_bp_added_per_division. Will senesce after around 45 divisions.

```sh
It is division # 49
This is the current list of telomere lengths: 
[7170, 12368, 5720, 3645, 5542, 12080, 5087, 11904, 11511, 6398, 3277, 10844, 2991, 7629, 8780, 6831, 6536, 7344, 3558, 7683, 3835, 8217, 6984, 8453, 5396, 4522, 4119, 12548, 9305, 9545, 9008, 7613, 9990, 12347, 7924, 9842, 5634, 5140, 3076, 9589, 9017, 6847, 12525, 7593, 7447, 8598, 7191, 5782, 8152, 12464, 5269, 6994, 3567, 7599, 11842, 4033, 5184, 10556, 5757, 7054, 11279, 6642, 11565, 10701, 11997, 3534, 3355, 11623, 10173, 8881, 3085, 11311, 6307, 8302, 11064, 10363, 3198, 9361, 3659, 4629, 6694, 12477, 3731, 3275, 10302, 7461, 7445, 5461, 11859, 9980, 8931, 11078]
Telomere number 4 is only 3645 bp long.
p53-mediated senescence would be triggered, BUT p53 is mutated!
Telomere number 11 is only 3277 bp long.
p53-mediated senescence would be triggered, BUT p53 is mutated!
Telomere number 13 is only 2991 bp long.
There is massive genomic instability and cell death!
```

This is what happend when I left it alone for a little while with a telomerase_bp_added_per_division = 6*767. It got up to division number 18,601! That's what people mean when they talk about cancer "immortality." 

ADD IMMORTALIZATION NOTE
Henson 2010 Assaying and investigating Alterantive Lengtheing of telomeras activity ijn human cells and cancers
a useful confirmatory test is to demonstrate that the cells being studied are in fact immortalized. This is usually done by determining whether the cells are able to grow in culture for >100 PD.

```sh
It is division # 18601
This is the current list of telomere lengths: 
[10252, 10250, 10248, 10252, 10251, 10250, 10252, 10248, 10249, 10250, 10249, 10251, 10249, 10250, 10249, 10252, 10248, 10251, 10250, 10248, 10250, 10248, 10251, 10247, 10248, 10252, 10247, 10252, 10250, 10247, 10247, 10249, 10252, 10248, 10247, 10252, 10250, 10251, 10251, 10248, 10246, 10248, 10251, 10246, 10250, 10249, 10247, 10247, 10246, 10251, 10249, 10250, 10251, 10246, 10248, 10247, 10251, 10248, 10249, 10250, 10246, 10248, 10246, 10248, 10250, 10248, 10251, 10249, 10251, 10246, 10250, 10251, 10247, 10250, 10247, 10247, 10246, 10251, 10251, 10251, 10250, 10248, 10246, 10249, 10249, 10249, 10246, 10246, 10250, 10246, 10250, 10249]
```

ADD SHAY 2016 FIGURE 2 ABOUT TMM IMMORTALIATIONS



Here's half of that number of telomerase hexamers with telomerase_bp_added_per_division = 6*383.

```sh
It is division # 264
This is the current list of telomere lengths: 
[2992, 2994, 2995, 2991, 2992, 2993, 2992, 2990, 2991, 2995, 2993, 2992, 2991, 2994, 2995, 2991, 2990, 2990, 2991, 2994, 2992, 2992, 2994, 2993, 2994, 2994, 2993, 2992, 2995, 2992, 2992, 2994, 2990, 2990, 2993, 2995, 2993, 2989, 2994, 2994, 2993, 2993, 2990, 2994, 2990, 2989, 2992, 2991, 2991, 2990, 2991, 2993, 2994, 2989, 2989, 2992, 2994, 2991, 2991, 2989, 2994, 2991, 2992, 2993, 2989, 2989, 2992, 2989, 2993, 2992, 2992, 2991, 2989, 2993, 2991, 2989, 2993, 2991, 2990, 2992, 2990, 2992, 2992, 2991, 2993, 2989, 2992, 2993, 2991, 2994, 2989, 2992]
Telomere number 1 is only 2992 bp long.
There is massive genomic instability and cell death!
```

Remember the wild range of telomere lengths from before? I made a new bar graph with these numbers. Notice how they've all settled out!

![Equal_Telomere_Shortening_Bar_Graph.jpg](/Assets/Equal_Telomere_Shortening_Bar_Graph.jpg "Equal_Telomere_Shortening_Bar_Graph.jpg")

NOTE: THE RANGE OF TELOMERE LENGTHS ISN'T NECESSARILY WHAT I HAVE DEPICTED HERE. I NEED TO TAKE SUDA 2002 INTO ACCOUNT IN A FUTURE UPDATE. ALSO Graakjaer 2003 The pattern of chromosome-specific variations in telomere length in humans is determined by inherited, telomere-near factors and is maintained throughout life FINDS THAT TELOMERASE DOES NOT CHANGE THE OVERALL LENGTH RANGE ... I SHOULD UPDATE THE MODEL TO ACT ON THE SHORTEST TELOMERES ***RELATIVE*** TO THE OVERALL LENGTH ... LIKE NORMALZING THEM TO EACHOTHER OR SOMETHING ... MATH IS HARD, LOL. GRAAKJAER 2003 ALSO FOUND A CORRELATION BETWEEN CHROMOSOME LENGTH AND TELOMERE LENGTH

#### Modeling the Single Stranded G-rich Tail
Another thing that I left out of earlier models was the G-rich and C-rich strands. I've just been describing the telomeres as having a length. They have sequence too! The G-rich strand is 5'-GGTTAG-3' and the C-rich strand is 3'-CCAATC-5'. Telomerase adds 5'-GGTTAG-3' (Harley 2008). The telomerase enzyme TERT uses the telomerase RNA 3'-CAAUCCCAAUC-5' as a template for the extension (Gavory 2002). There is a G-rich single stranded telomeric overhang of 130-210 nucleotides (Cesare 2010).

I made a simple model of the G'rich overhang in R.

```r
setwd("/media/david/Linux/ALT_Introns_Exons_and_Promoters/Telomere_Math_Models")
library(msa)
library(seqinr)
G_overhang_sequence <- "GGTTAG"
C_overhang_sequence <- "CCAATC"
reverse_complement_C_overhang_sequence <- "CTAACC"
# 22*6 = 132 (min single stranded overhang is 130)
# assuming 10 kbp telomere lengths, so 1666 * 6 9996 is for C strand
# then 1666+22 is for G strand
full_G_overhang_sequence <- paste(replicate(1688, G_overhang_sequence), collapse = "")
full_C_overhang_sequence <- paste(replicate(1666, reverse_complement_C_overhang_sequence), collapse = "")
write.fasta(sequences = full_G_overhang_sequence, names = "full_G_overhang_sequence", file.out = "full_G_overhang_sequence.fasta", open = "w", nbchar = 70, as.string = FALSE)
write.fasta(sequences = full_C_overhang_sequence, names = "full_C_overhang_sequence", file.out = "full_C_overhang_sequence.fasta", open = "w", nbchar = 70, as.string = FALSE)
```

I can't figure out how to make a pretty DNA complementary base pairing figure ... any ideas? Please let me know :) I made a simple, shortened, text version:

![G_overhang](/Assets/G_overhang.jpg "G_overhang")

NOTE: I NEED TO MAKE SURE I'VE GOT THE RIGHT NUMBER FOR TELOMERE VS. SUBTELOMERE ... CHECK RESTRICTION ENZYME DATA AND READ THESE TWO PAPERS: 
Riethman 2004 Mapping and Initial Analysis of Human Subtelomeric Sequence Assemblies
Riethman 2009 Human subtelomeric copy number variations
Mefford 2002 The complex structure and dynamic evolution of human subtelomeres
Suda 2002 Interchromosomal Telomere Length Variation
Graakjaer 2003 The pattern of chromosome-specific variations in telomere length in humans is determined by inherited, telomere-near factors and is maintained throughout life

TALK ABOUT POT1 ALLOW TELOMERASE FROM LEI 2005 FIG 7

#### Model of Inhibiting Telomerase 
When DNA is getting copied, small end pieces aren't able to be fully copied. This is known as the End Replication Problem and is a result of Okazaki fragments incompletely covering the end of the chromosome. This is an issue for cell types that need to divide a lot, like Hematopoietic stem cells (HSC). HSCs have plenty of division to do so they can keep up with all the differentiation to make blood cells. This is why they express telomerase, which is a reverse transcriptase that adds repetitive telomeric DNA (TTAGGG)n to the ends of the chromosomes (Allsopp 2001). Did you notice that I'm citing a paper from the Weissman lab? ;)  
 
![telomeres-shorten-with-age](/Assets/telomeres-shorten-with-age.jpg "telomeres-shorten-with-age")

(Finkel 2007)

Cells that divide a lot will senesce in the absence of an active telomere maintenance mechanism (Shay 2012). That's why Telomerase is great for stem cells and other cell types that need to divide a lot. HOWEVER, it's also part of how the majority of cancers become immortal (Cesare 2010). This is why several companies are working on telomere-based anti-cancer therapies:

* Telomerase enzyme inhibitor: 
	* GRN163L (Geron)
* Telomerase active immunotherapy:	
	* GRNVAC1 (Geron)
	* GV1001 (Pharmexa)
	* P540-548 (Gemvax)
	* Vx01 (Vaxon Biotech)
	* TLI (Cosmo Bioscience) 

(Shay 2012, Harley 2008)

This model is the same as the telomere shortening + telomerase model AND you can choose a cell division number for telomerase to be inhibited at. There are two scenarios that I want to model:

1) cancers with relatively short telomeres (these will divide out without telomerase)
2) cancers with very long telomeres (these might be able to keep dividing in the absence of telomerase)
3) cancers with telomeres that are equilavent to stem cell telomeres (anti-telomerase therapy will exhaust the stem cell pools before the cancer)

I bring up point 3 because one problem with telomerase inhibitors is that they have been reported to cause problems with blood stem cells (Hu 2017). This update only needed three lines of code. I added a varible for the division number for telomerase to stop at and an if condition that sets telomerase activity to 0 AFTER that division number has been reached. 

ADD THESE TO ANTI-TELOMERASE STEM CELL ISSUES
In addition, because some hematopoietic proliferative cells
exert regulated telomerase activity, toxicities have been observed
( 100–102 ), such as thrombocytopenia (e.g., low platelet counts).
These toxicities require patients to go off the telomerase inhibi-
tor, and very quickly the telomeres regain their length.
Chiappori AA , Kolevska T , Spigel DR , Hager S , Rarick M , Gadgeel
S , et al. A randomized phase II study of the telomerase inhibitor
imetelstat as maintenance therapy for advanced non-small-cell lung
cancer . Annal Oncol 2015 ; 26 : 354 – 62 .
101. Baerlocker GM , Leibundgut EO , Ottmann OG , Spitzer G , Odenike
O , McDivitt MA , et al. Telomerase inhibitor imetelstat in patients
with essential thrombocythemia . New Engl J Med 2015 ; 373 : 920 – 8 .
102. Tefferi A , Lasho TL , Begna KH , Patnaik MM , Zblewski DL , Finke
CM , et al. A pilot study of the telomerase inhibitor imetelstat for
myelofi brosis . New Engl J Med 2015 ; 373 : 908 – 19 .
ADD THESE TO ANTI-TELOMERASE STEM CELL ISSUES

```python
telomerase_stopped_at_division_number = 30
telomere_bp_left_to_add = telomerase_bp_added_per_division
    if telomerase_stopped_at_division_number <= current_division_number:
        telomere_bp_left_to_add = 0
    while telomere_bp_left_to_add > 0:
        # get index for shortest telomere
        shortest_telomere_index = current_list_of_telomere_lengths.index(min(current_list_of_telomere_lengths))
        # get length of shortest telomere
        length_of_shortest_telomere = current_list_of_telomere_lengths[shortest_telomere_index]
        # add 6bp to shortest telomere
        new_length_of_shortest_telomere = current_list_of_telomere_lengths[shortest_telomere_index] + 6
        # change list entry at index # to new telomere length
        current_list_of_telomere_lengths[shortest_telomere_index]=new_length_of_shortest_telomere
        # less telomerase left
        telomere_bp_left_to_add = telomere_bp_left_to_add - 6
    # setting up for next division
    current_list_of_telomere_lengths = [telomere-50 for telomere in current_list_of_telomere_lengths]
    current_division_number += 1
```

NOTE: I SHOULD CHANGE THE CODE TO HAVE A TELOMERE LENGTH SEEDING NUMBER. IT'S CURRENTLY GETTING LONG TELOMERE LENGTHS BY HAVING A HIGH INITIAL TELOMERASE LEVEL AND THE TELOMERASE INHIBITION STARTED AT LATER CELL DIVISIONS. THE CONCEPTS ARE THE SAME, BUT IT'S NOT AS ELEGANT. I SHOULD ALSO ADD A STEM CELL TELOMERE LENGTH FOR THE STEM CELL PROBLEMS OF ANTI-TELOMERASE. I NEED TO GET AN ESTIMATE OF CANCER GROWTH OVER DIVISION NUMBER, SO I CAN ADD THAT TO THE SHORT TELOMERE CANCER INHIBITION CASE.

Cancers with relatively short telomeres (these will divide out without telomerase):

```sh
It is division # 72
This is the current list of telomere lengths: 
[5309, 3215, 8597, 6167, 5741, 11130, 7328, 2978, 7239, 4484, 6188, 5785, 3948, 2978, 4771, 4212, 3670, 10457, 10790, 2975, 2976, 10914, 7447, 7491, 3936, 9322, 3866, 7015, 2978, 2978, 7193, 3883, 10189, 5269, 7772, 9935, 9335, 5016, 8568, 3551, 4133, 2976, 4655, 5280, 2975, 7598, 6102, 3259, 2977, 2979, 11118, 2977, 4284, 9731, 2978, 2979, 7753, 8627, 3875, 4769, 9755, 9210, 3822, 5761, 3288, 10555, 6506, 4434, 4774, 9741, 3911, 2980, 4942, 7019, 4712, 2976, 9085, 3298, 6611, 2980, 10056, 3279, 9046, 2978, 8006, 4973, 8171, 8519, 6429, 10526, 10572, 4949]
Telomere number 2 is only 3215 bp long.
p53-mediated senescence would be triggered, BUT p53 is mutated!
Telomere number 8 is only 2978 bp long.
There is massive genomic instability and cell death!
```

Cancers with very long telomeres (these might be able to keep dividing in the absence of telomerase). telomerase_stopped_at_division_number = 600 AND telomerase_bp_added_per_division = 6*767

```sh
It is division # 737
This is the current list of telomere lengths: 
[2988, 2986, 2988, 2984, 2985, 2984, 2987, 2986, 2985, 2984, 2985, 2986, 2987, 2988, 2984, 2989, 2989, 2985, 2987, 2985, 2986, 2986, 2987, 2985, 2987, 2989, 2988, 2988, 2985, 2984, 2988, 2985, 2988, 2988, 2988, 2986, 2986, 2985, 2984, 2986, 2986, 2983, 2983, 2984, 2986, 2986, 2988, 2988, 2985, 2985, 2983, 2983, 2984, 2985, 2984, 2988, 2983, 2984, 2983, 2987, 2988, 2986, 2984, 2983, 2985, 2984, 2986, 2984, 2988, 2985, 2983, 2984, 2983, 2988, 2985, 2988, 2988, 2987, 2988, 2988, 2987, 2988, 2985, 2987, 2986, 2986, 2987, 2985, 2986, 2985, 2988, 2983]
Telomere number 1 is only 2988 bp long.
There is massive genomic instability and cell death!
```

# Alternative Lengthening of Telomeres (ALT) Extends Telomeres
Stem cell telomerase isn't the only problem with the telomerase inhibition approach. Approximately 10-15% of cancers use the Alterantive Lengthening of Telomeres (ALT) to extend telomeres, some cancers won't be treated with these anti-telomerase therapies. But, it's way worse of a problem than that! Tumors have been reported to use both ALT and TEL simultaneously (Gocha 2013) AND in vitro inhibition of telomerase selects for ALT activity (Sahin 2012). 

![TEL_ALT_Reversible](/Assets/TEL_ALT_Reversible.jpg "TEL_ALT_Reversible")

(Shay 2012)

On an interesting note, there is a high frequency of cancers with a Mesenchymal Stem Cell origin using the ALT pathway (77% malignant fibrous histocytomas, 47-66% of osteosarcomas (Lafferty-Whyte 2009), 21.4% of liposarcomas (Venturini APB ALT LIPOSARCOMA 2008). This may be a result of the telomerase promoter being repressed with chromatin compaction (Atkinson 2005). Telomerase inhibition MIGHT not be alone in potentially causing problems for stem cells. There is some evidence to suggest that stem cells use ALT (Kalmbach 2014, Huang 2014). To make things worse, some cancers appear to extensively divide without a telomere maintenance mechanism (Dagg 2017).  

![stem_cell_ALT.jpg](/Assets/stem_cell_ALT.jpg "stem_cell_ALT.jpg")

(Kalmbach 2014)

#### ALT Telomeres are Long and Heterogenous
ALT telomeres have long, heterogenous telomeres. They can range from less than 1 kbp (Rogan 1995) all the way up to 50 kbp (Bryan 1995). There is a rapid addition of telomeric sequences to short telomeres AND a rapid deletion of telomeric sequences from the long telomeres. This suggests recombinogenic behavior (Murnane 1994). ALT cells seem to be extending their telomeres through this process, but the mechanism isn't completely understood yet (Cesare 2010).  

I think there are still more details that I should take into account for this idea, but I'm not sure when I'll have the time for that. The simplified model I have in mind will:

1) range in initialized telomere length from 500 bp to 50,000 bp
2) have rapid kbp exchanges between short and long telomeres
3) result in overall telomere extension on the short telomeres that are on the recombinogenic receiving end

```python
# I HAVEN'T MADE THIS YET.
```

ADD ALT TELOMRE LENGTH MODEL INOFRMATION
(TRF data) ALT telomere length modal length approximately twice that in comparable telomerase[+] or normal cells [3], [26].
3 is Bryan 1995. ALT up to 50 kb (peaks at 10 and 50 kb). Telomerase-negative cell lines do not contain inhibitor(s) of telomerase or Taq polymerase.  IIICF/c TRF pattern was not detected until around 40 PD after immortalization.  
T.M. Bryan, A. Englezou, J. Gupta, S. Bacchetti, R.R. Reddel
Telomere elongation in immortal human cells without detectable telomerase activity
EMBO J., 14 (1995), pp. 4240-4248
L.S. Gollahon, E. Kraus, T.A. Wu, S.O. Yim, L.C. Strong, J.W. Shay, M.A. Tainsky
Telomerase activity during spontaneous immortalization of Li-Fraumeni syndrome skin fibroblasts
Oncogene, 17 (1998), pp. 709-717

The telomere length heterogeneity can also be visualized in metaphase spreads by telomere fluorescence in situ hybridization (FISH) [14].
K. Perrem, L.M. Colgin, A.A. Neumann, T.R. Yeager, R.R. Reddel
Coexistence of alternative lengthening of telomeres and telomerase in hTERT-transfected GM847 cells
Mol. Cell. Biol., 21 (2001), pp. 3862-3875  

Telomere lengths in ALT cells are not normally distributed, in contrast to telomerase[+] cells, most of which regulate their telomere lengths about a mean of 5–10 kb [27], [28].
27 is Henson 2002. normal telomeres 15kb in human germline. somatic cells in vitro TRF length declines rate 40-200 bp/cell division down to 5-8 kb at senesnce. . most tleloemrase positive lines TRF lengths are erelatively homogenous w/ mean length usually less than 10 kb. ALT mean is around 20kb and TRF lengths range from less than 3kb to over 50 kb. 
J.D. Henson, A.A. Neumann, T.R. Yeager, R.R. Reddel
Alternative lengthening of telomeres in mammalian cells
Oncogene, 21 (2002), pp. 598-610
28 is Jeyapalan 2008. TRF telomrees are 0.5 kb to >40 kb.
Jeyapalan 2008 Evidence for alternative lengthening of telomeres in liposarcomas in the absence of ALT‐associated PML bodies

single telomeres in ALT[+] cells revealed sporadic, unsynchronized increases and decreases in telomere lengths of a variable amount (that are sometimes very large – up to ∼20 kb) on a background of gradual erosion (∼50 bp/PD) [29], which appear to be responsible for the broad distribution of ALT telomere lengths [28].
29 is Murnane 1994
J.P. Murnane, L. Sabatier, B.A. Marder, W.F. Morgan
Telomere dynamics in an immortal human cell line
EMBO J., 13 (1994), pp. 4953-4962
28 is J.N. Jeyapalan, A. Mendez-Bermudez, N. Zaffaroni, Y.E. Dubrova, N.J. Royle
Evidence for alternative lengthening of telomeres in liposarcomas in the absence of ALT-associated PML bodies
Int. J. Cancer, 122 (2008), pp. 2414-2421

his pattern is established within one PD (equivalent to approximately 17 cell generations, which are required for one clone to overgrow a culture that is in crisis) of ALT being activated during immortalization in vitro [30].
T.R. Yeager, A.A. Neumann, A. Englezou, L.I. Huschtscha, J.R. Noble, R.R. Reddel
Telomerase-negative immortalized human cells contain a novel type of promyelocytic leukemia (PML) body
Cancer Res., 59 (1999), pp. 4175-4179

The long heterogeneous telomere length pattern remains the best-established marker for ALT in human cells, including tumors archived under conditions where it is possible to extract high-quality genomic DNA [5], [31]. 
5 is T.M. Bryan, A. Englezou, L. Dalla-Pozza, M.A. Dunham, R.R. Reddel
Evidence for an alternative mechanism for maintaining telomere length in human tumors and tumor-derived cell lines
Nat. Med., 3 (1997), pp. 1271-1274
31 is J.D. Henson, J.A. Hannay, S.W. McCarthy, J.A. Royds, T.R. Yeager, R.A. Robinson, S.B. Wharton, D.A. Jellinek, S.M. Arbuckle, J. Yoo, B.G. Robinson, D.L. Learoyd, P.D. Stalley, S.F. Bonar, D. Yu, R.E. Pollock, R.R. Reddel
A robust assay for alternative lengthening of telomeres (ALT) in tumors demonstrates the significance of ALT in sarcomas and astrocytomas
Clin. Cancer Res., 11 (2005), pp. 217-225

Long and/or heterogeneous telomeres are seen in telomerase[+] cell lines when expression of hTR or hTERT at supra-physiological levels challenges the telomere length regulatory mechanism with excessive telomere lengthening [32], [33].
Y. Cao, L.I. Huschtscha, A.S. Nouwens, H.A. Pickett, A.A. Neumann, A.C. Chang, C.D. Toouli, T.M. Bryan, R.R. Reddel
Amplification of telomerase reverse transcriptase gene in human mammary epithelial cells with limiting telomerase RNA expression levels
Cancer Res., 68 (2008), pp. 3115-3123
H.A. Pickett, A.J. Cesare, R.L. Johnstone, A.A. Neumann, R.R. Reddel
Control of telomere length by a trimming mechanism that involves generation of t-circles
EMBO J., 28 (2009), pp. 799-809

Conversely, it may not be necessary for cells using the ALT mechanism to have long telomeres [34].
M.A. Cerone, C. Autexier, J.A. Londono-Vallejo, S. Bacchetti
A human cell line that maintains telomeres in the absence of telomerase and of key markers of ALT
Oncogene, 24 (2005), pp. 7893-78901

Up to 30% of chromosome ends in ALT cells have been reported as having undetectable telomeres [51] and even some easily detectable ALT telomeres may be “functionally short” due to an increased number of variant telomeric repeats [28], [66], [77], [93].
51 is T. Jegou, I. Chung, G. Heuvelman, M. Wachsmuth, S.M. Gorisch, K.M. Greulich-Bode, P. Boukamp, P. Lichter, K. Rippe
Dynamics of telomeres and PML nuclear bodies in a telomerase negative human cell line
Mol. Biol. Cell, 20 (2009), pp. 2070-2082
28 is J.N. Jeyapalan, A. Mendez-Bermudez, N. Zaffaroni, Y.E. Dubrova, N.J. Royle
Evidence for alternative lengthening of telomeres in liposarcomas in the absence of ALT-associated PML bodies
Int. J. Cancer, 122 (2008), pp. 2414-2421
66 is J.D. Henson, Y. Cao, L.I. Huschtscha, A.C. Chang, A.Y. Au, H.A. Pickett, R.R. Reddel
DNA C-circles are specific and quantifable markers of alternative-lengthening-of-telomeres activity
Nat. Biotechnol., 27 (2009), pp. 1181-1185
77 is 
H. Varley, H.A. Pickett, J.L. Foxon, R.R. Reddel, N.J. Royle
Molecular characterization of inter-telomere and intra-telomere mutations in human ALT cells
Nat. Genet., 30 (2002), pp. 301-305
J. Dejardin, R.E. Kingston
Purification of proteins associated with specific genomic loci
Cell, 136 (2009), pp. 175-186

ADD TELOOMERE SHORTENING EXAMPLE
hENSON 2010 Assaying and investigating Alternative Lengthening of Telomeres activity in human cells and cancers
For example, in an ALT[+] fibroblast cell line in which the MRE11/RAD50/NBS1 (MRN) complex was sequestered following expression of high levels of SP100 protein, telomere length declined linearly (over several time-points) at a rate of approximately 120 base pairs (bp)/PD.

a useful confirmatory test is to demonstrate that the cells being studied are in fact immortalized. This is usually done by determining whether the cells are able to grow in culture for >100 PD.

#### ALT Telomeres Have C-rich Overhangs
There is some degree of 5' C-rich overhang in ALT cells. 


Min 2015 Alternative lengthening of telomeres can be maintained by preferential elongation of lagging strands
Overhang
length in SW39 ALT1 cells are variable from 40 nt to 400 nt,
whereas parental SW39 cells have 65 nt to 140 nt overhang
lengths consistent with previous reports (overhang length
in telomerase positive cells: 60–150 nt)
Min 2015 Alternative lengthening of telomeres can be maintained by preferential elongation of lagging strands

![C_overhang](/Assets/C_overhang.jpg "C_overhang")

^I need to do a bit more reading to make an accurate model of this. Here are some good papers to check out:

* Oganesian 2011 Mammalian 5 0 C-Rich Telomeric Overhangs Are a Mark of Recombination-Dependent Telomere Maintenance
* Min 2017 Alternative lengthening of telomeres can be maintained by preferential elongation of lagging strands
* Mao 2016 Homologous recombination-dependent repair of telomeric DSBs in proliferating human cells

The altered C-rich overhangs involved in ALT will likely prevent POT-1 from binding effectively to the telomeres. This is a great segway into the ALT literature! For example, POT-1 deficiency creates ALT in C. elegans!

# POT-1 Deficiency Creates ALT+ C. Elegans Strains
Telomeres cap linear chromosomes because DNA polymerase can't completely copy chromosomes. Telomerase adds telomeric repeats to the ends of linear chromosomes with reverse transcription. Most human cancers have long, heterogenous telomeres. Telomere shortening leads to senescence and potentially crisis. Cancer emerges as part of massive cell death and genomic rearrangements after crisis. 10-15% of cancers are estimated to use ALT (Cheng 2012). 

ALT can happen in Caenorhabditis elegans! Mammalian POT1 has homologs in C. elegans as pot-1 (CeOB2) and pot-2 (CeOB1). What's the deal with the reversing of 1 and 2? That's how it's reported in the paper ... it's odd. pot-1 mutant C. elegans have HUGE telomere lengths while pot-2 mutants have normal telomere lengths. The authors of Cheng 2012 created a variety of mutants in C. elegans.  The trt-1 C. elegans mutant has a deletion in telomerase reverse transcriptase. trt-1 & pot-2 absence led to ALT+ Caenorhabditis elegans with normal telomere lengths. trt-1 and pot-1 mutants were found to have long, heterogenous telomere lengths like those seen in human ALT. Here is the survival figure showing that C. elegans can survive in the absence of telomerase reverse transcriptase.

![Celegans_ALT_Generation_Survival](/Assets/Celegans_ALT_Generation_Survival.jpg "Celegans_ALT_Generation_Survival")

(Cheng 2012)

#### Multiple Sequence Alignment of pot-1 Genes
YES, pot-2 was the central point of the paper, but it won't be as fun to play with because it only has one isoform. I picked pot-1 cause there is a lot of cool stuff to play with. There were a lot of workup steps to get all of the sequences ... It would take a long while to review them. Essentially, I looked up the proteins on UniProt and then grabbed the DNA files from NCBI GenBank and WormBase. Check out the Celegans_POT1_ALT folder for the file names of everything. The file containing all the C. elegans genes is Celegans_POT1_genes.fasta. I used the R package "msa" for multiple sequence alignment with this code:

```r
library(msa)
Celegans_POT1_genes <- "/media/david/Linux/Introns_Exons_and_Promoters/Celegans_POT1_ALT/DNA/Celegans_POT1_genes.fasta"
Celegans_POT1_genes_DNA <- readDNAStringSet(Celegans_POT1_genes)
Celegans_POT1_gene_alignment <- msa(Celegans_POT1_genes_DNA)
msaPrettyPrint(Celegans_POT1_gene_alignment, output="pdf", showNames="none",
showLogo="none", askForOverwrite=FALSE, verbose=FALSE)
```

The aligned sequences aren't very pretty ... I decided not to include sequence labels cause it shortened the available nucleotide space for each new line. Here's part of the output for you to get the idea of the work:

![Celegans_POT1_gene_alignment](/Assets/Celegans_POT1_gene_alignment.jpg "Celegans_POT1_gene_alignment")

#### Multiple Sequence Alignment of pot-1 Proteins
I grabbed all the C elegans pot-1 isoform sequences from UniProt. You can check them out in Celegans_POT1_ALT/Protein. The file containing all of the sequences is Celegans_POT1_Proteins.fasta. I aligned all of the proteins with code that is similar to the DNA alignment code:

```r
Celegans_POT1_proteins <- "/media/david/Linux/Introns_Exons_and_Promoters/Celegans_POT1_ALT/Protein/Celegans_POT1_Proteins.fasta"
Celegans_POT1_proteins_AA <- readAAStringSet(Celegans_POT1_proteins)
Celegans_POT1_protein_alignment <- msa(Celegans_POT1_proteins_AA)
Celegans_POT1_protein_alignment
msaPrettyPrint(Celegans_POT1_protein_alignment, output="pdf", showNames="none",
showLogo="none", askForOverwrite=FALSE, verbose=FALSE)
```

This alignment looks great! You can see all of the alignments between the different pot-1 isoforms :)

![Celegans_POT1_protein_alignment](/Assets/Celegans_POT1_protein_alignment.jpg "Celegans_POT1_protein_alignment")

#### Displaying pot-1 Open Reading Frames
I used code from the BioPython Tutorial to identify the C. elegans pot-1 gene Open Reading Frames AND to report the translated proteins! Compare this to the last section to see that the the DNA -> Protein translations all have the correct lengths! The code is from http://biopython.org/DIST/docs/tutorial/Tutorial.html in the section titled "20.1.13. Identifying open reading frames". You should check this code out! It can identify Open Reading Frames in the +/- strand AND in three different reading frames, SO IT DOES ALL 6 FRAMES!!! I re-used the code four times (instead of making a function, haha). Here's part of the code that I used:

```python
#!/usr/bin/env python

from Bio import SeqIO
# record = SeqIO.read("NC_005816.fna", "fasta")
file_0 = "NM_001361730.1_Caenorhabditis_elegans_pot-1_gene_homolog.fasta"
file_1 = "NM_001361731.1_Caenorhabditis_elegans_pot-1_gene_homolog.fasta"
file_2 = "NM_001361732.1_Caenorhabditis_elegans_pot-1_gene_homolog.fasta"
file_3 = "NM_066157.3_pot-1_NCBI_DNA_matchesP42001_Celegans.fasta"

print("")
print("NM_001361730.1_Caenorhabditis_elegans_pot-1_gene_homolog.fasta")
record = SeqIO.read(file_0, "fasta")
table = 11
min_pro_len = 150

for strand, nuc in [(+1, record.seq), (-1, record.seq.reverse_complement())]:
    for frame in range(3):
        length = 3 * ((len(record)-frame) // 3) #Multiple of three
        for pro in nuc[frame:frame+length].translate(table).split("*"):
            if len(pro) >= min_pro_len:
                print("%s...%s - length %i, strand %i, frame %i" \
                % (pro[:30], pro[-3:], len(pro), strand, frame))
```

![Displaying_pot-1_Open_Reading_Frames](/Assets/Displaying_pot-1_Open_Reading_Frames.jpg "Displaying_pot-1_Open_Reading_Frames")

#### Discussing C. elegans pot-1 Alternative Splicing
WormBase has three isoforms for pot-1 in C. elegans https://wormbase.org/species/c_elegans/gene/WBGene00015105#0-9g-3

![WormBase_pot-1_Celegans_Isoforms](/Assets/WormBase_pot-1_Celegans_Isoforms.jpg "WormBase_pot-1_Celegans_Isoforms")

Transcript B0280.10a.1 is 1216 nucleotides in length and codes for a 400 amino acid protien. The WormBase curators used RNA-seq data from Boeck 2016 to alter the original WormBase entry to include the published alternate intron splicing. You can see from the table that Exons 1-10 are part of this pot-1 isoform.

![B0280.10a.1_Celegans_pot-1_isoformA_1203NT_400AA](/Assets/B0280.10a.1_Celegans_pot-1_isoformA_1203NT_400AA.jpg "B0280.10a.1_Celegans_pot-1_isoformA_1203NT_400AA")

Transcript B0280.10b.1 is 462 nucleotides in length and it codes for a 153 amino acid protein. You can see from the table that Exons 1-4 are part of this pot-1 isoform. Boeck 2016 goes into more detail about the alternative intron that causes alternative splicing here. 

![B0280.10b.1_Celegans_pot-1_isoformB_462NT_153AA](/Assets/B0280.10b.1_Celegans_pot-1_isoformB_462NT_153AA.jpg "B0280.10b.1_Celegans_pot-1_isoformB_462NT_153AA")

Transcript B0280.10c.1 is 1140 nucleotides long and it codes for a 379 amino acid protein. You can see from the table that Exons 1-10 make it into this protein isoform.

![B0280.10c.1_Celegans_pot-1_isoformC_1140NT_379AA](/Assets/B0280.10c.1_Celegans_pot-1_isoformC_1140NT_379AA.jpg "B0280.10c.1_Celegans_pot-1_isoformC_1140NT_379AA")

# ATRX Exon Deletion is Common in ALT
This project can be found in the Human_ATRX_ALT folder. ATRX gene mutations are found in a range of cancers. 10-15% of cancers are estimated to use ALT. ALT involves homologous recombination-based telomere elongation. Inactivating mutations in either ATRX or DAXX are found in many cancers. Depletion of ATRX seems insufficient to trigger ALT, but it does seem to play a key role in the ALT pathway. The absence of ATRX might lead to the failure of stalled replication forks to get resolved. The required fork restart would require homologus recombination and could jumpstart the ALT pathway (Clynes 2013). ALT involves a template-based lengthening of telomeres with homologous recombination. The genetic and epigenetic changes are not full understood. Lovejoy 2012 reported that ATRX gene mutations are a common feature of ALT. Specifically 19/22 ALT+ cell lines had an issue with the expression of ATRX or DAXX (Lovejoy 2012). See the Lovejoy 2012 supplementary information for the Excel table of Exon deletions in ALT cell lines. 

ADD REN 2018 FIGURE 1 OF EXON DELETIONS REPORTED BY THE LITERATURE

![ATRX_Prevents_Fork_Collapse](/Assets/ATRX_Prevents_Fork_Collapse.jpg "ATRX_Prevents_Fork_Collapse")

(Clynes 2013)

#### Getting ATRX DNA
Searching Ensembl for human ATRX yielded ATRX-201 and ATRX-202. I picked ATRX-201 cause it has 35 exons (which matches the Lovejoy 2012 paper). It was Ensembly ENST00000373344.10. Ensembl refseq switch to NCBI Reference Sequence yielded NM_000489.5 for the gene. I saved it as NM_000489.5_homo_sapiens_ATRX_Gene.fasta.

#### Removing ATRX Exons 2-29 
See the Lovejoy 2012 supplementary Excel table for a list of commonly missing ATRX Exons. I decided to play with the U2OS variant because that is a cell line that I used to grow :) U2OS is missing ATRX exons 2-29. NCBI says exon 2 is [236:348] and exon 29 is 6542..6719 https://www.ncbi.nlm.nih.gov/nuccore/NM_000489. I used R to remove those exons.

```r
library(seqinr)
WT_hATRX_Gene <- read.fasta("NM_000489.5_homo_sapiens_ATRX_Gene.fasta")
WT_hATRX_Gene_Nucleotides <- WT_hATRX_Gene[[1]]
length(WT_hATRX_Gene_Nucleotides)
typeof(WT_hATRX_Gene_Nucleotides)
WT_hATRX_Gene_Nucleotides
U2OS_hATRX_Gene_Nucleotide_FIRST <- WT_hATRX_Gene_Nucleotides[1:235]
U2OS_hATRX_Gene_Nucleotide_SECOND <- WT_hATRX_Gene_Nucleotides[6720:length(WT_hATRX_Gene_Nucleotides)]
U2OS_ATRX_Characters <- c(U2OS_hATRX_Gene_Nucleotide_FIRST, U2OS_hATRX_Gene_Nucleotide_SECOND)
U2OS_ATRX_DNAstring <- DNAString(paste(toupper(U2OS_ATRX_Characters), collapse = ""))
```

#### Sequence Alignment of WT ATRX to Mutant ATRX
The R msa package can't handle the full length of the ATRX gene, so I shortened it down to 400 nucleotides.
```{r}
# limit it to 400 ... that's more than enough to see exon absence
U2OS_ATRX_DNA_Short <- U2OS_ATRX_DNAstring[1:400]
WT_hATRX_DNA_Short <- toupper(WT_hATRX_Gene_Nucleotides[1:400])
write.fasta(sequences = U2OS_ATRX_DNA_Short, names = "U2OS_ATRX_DNA_Short", file.out = "U2OS_ATRX_DNA_Short.fasta", open = "w", nbchar = 70, as.string = FALSE)
write.fasta(sequences = WT_hATRX_DNA_Short, names = "WT_hATRX_DNA_Short", file.out = "WT_hATRX_DNA_Short.fasta", open = "w", nbchar = 70, as.string = FALSE)
library(msa)
# both_ATRX_Sequences <- read.fasta("WT_and_U2OS_hATRX.fasta")
both_ATRX_Sequences_SHORT <- "both_ATRX_Sequences_SHORT.fasta"
# typeof(both_ATRX_Sequences)
#both_ATRX_DNAStringSet <- readDNAStringSet(both_ATRX_Sequences)
#both_ATRX_Sequences_Alignment <- msa(both_ATRX_DNAStringSet)
both_ATRX_Sequences_SHORT_StringSet <- readDNAStringSet(both_ATRX_Sequences_SHORT)
both_ATRX_Sequences_Alignment_SHORT <- msa(both_ATRX_Sequences_SHORT_StringSet)
both_ATRX_Sequences_Alignment_SHORT
msaPrettyPrint(both_ATRX_Sequences_Alignment_SHORT, output="pdf", showNames="none",
showLogo="none", askForOverwrite=FALSE, verbose=TRUE)
#texi2pdf("both_ATRX_Sequences_Alignment.tex", clean=TRUE)
```
You can see that the sequences are the same until postion 236. That is where the Exon deletion for U2OS starts! 
![ATRX_Exon_Deletion_Alignment](/Assets/ATRX_Exon_Deletion_Alignment.jpg "ATRX_Exon_Deletion_Alignment")

# TERT Promoter Compaction is Found in ALT
ALT cells commonly have long, heterogenous telomere lengths (Kumakura 2005). Mouse embryonic stem cells deficient for DNMT have HUGE telomeres. Under normal conditions, mouse subtelomeres are heavily methylated, BUT that is not the case in mESC deficient for DNMT. The lack of DNMT increased the rate of telomeric sister chromatid exchanges (T-SCE), and ALT-associated Promyelocytic Nuclear Bodies (APBs). T-SCE and APBs are both common features of ALT activity. The authors concluded that the increased telomeric recombination MIGHT lead to telomere length changes, BUT they do not exclude the involvement of telomerase in the weirdly long telomeres that were seen (Gonzalo 2006). Luckily, I found these two other papers that go into more detail about TERT chromatin compaction in ALT!

Atkinson 2005 found that chromatin modifications of hTR and hTERT promoters were commonly found in ALT activity. Treatment of ALT+ cells with 5-AZC or Trichostatin A lead to chromatin remodeling of hTR and hTERT. This induced telomerase expression. Interestingly enough they found that mehtylated Lys20 Histon H4 was not associated with gene expression, BUT does seem to be ALT specific (Atkinson 2005). This might be a new marker of ALT activity! Acetylation of H3K9 and methylation of H3K4 is known to be associated with an open chromatin conformation. In Kumakura 2005, the authors found that ALT+ cells had H3K9 methylation and low levels of H3K4 methylation and H3K9+H3K14 acetylations. The ratio of H3K9 methylation / H3K4 methylation was different across ALT+ and TEL+ cell lines. They found that treating ALT+ cells with TSC or 5-AZC caused a reversion from complete to partial methylation of the CpG islands on the hTERT promoter. They switched an E6CL TEL+ line to TEL- and it was able to grow for well over 240 population doublings (Kumakura 2005). That's some ALT activity right there!
![H3K9_H3K4_Methylation_Ratio](/Assets/H3K9_H3K4_Methylation_Ratio.jpg "H3K9_H3K4_Methylation_Ratio")

(Kumakura 2005)

#### Getting The hTERT Sequence
The UniProt entry O14746 is for hTERT https://www.uniprot.org/uniprot/O14746. Following GeneID 7015 gets TERT telomerase reverse transcriptase for humans https://www.ncbi.nlm.nih.gov/gene/7015. Note that the reverse arrow on TERT indicates that the sequence is on the reverse strand (this will become important later). I downloaded the FASTA as "NC_000005.10_hChrom5_TERT_CpG_Start.fasta". A quick text search shows that the start codon is at position 59. Take care with this sequence cause it's the reverse complement of the actual sequence!

![hTERT_NCBI_Reverse_Strand](/Assets/hTERT_NCBI_Reverse_Strand.jpg "hTERT_NCBI_Reverse_Strand")

#### Obtaining hTERT WITH the CpG Island Region
Stay with me ... we're about to dig a bit into the literature! The hTERT sequence that I grabbed from NCBI DOES NOT contain the CpG island for hTERT. It doesn't even contain the normal promoter region for hTERT! Cong 1999 reports that the core hTERT promoter region is from -330 to +361 bp of the ATG start codon. HOWEVER, Kumakura 2005 found the hTERT CpG island to be from 654 bp upstream to 510 bp downstream of the ATG start codon, so this is the actual region that I need to grab! 

Grabbing the hTERT FASTA sequence from https://www.ncbi.nlm.nih.gov/gene/7015 INITIALLY is from: 1253167 to: 1295047. Checking Cong 1999 and The FASTA file, I can see that the hTERT start codon, AND a bit more of that region, of "ATGCCGCGCGCT" is at the end of the first FASTA line, which is 59 in from the left (59 is A of ATG). CpG is 654 bp upstream of the transcriptoin start site, SO going 595 back from current start site 1253167-595 = 1252572. 1252572 should be the start of the CpG island, RIGHT?!? WRONG!!! ... Why aren't I getting any more nucleotides before the current start read?!?!? OH!!! I'm looking at the reverse complement, lol! ;) 

It should be  1295047 + 595 = 1295642 YESSSSSSS, that's right :) Now I have more at the beginniig, so "atgccgcgcgctccccgct" is fully searchable! This is the new range:
https://www.ncbi.nlm.nih.gov/nuccore/NC_000005.10?report=fasta&from=1253167&to=1295642&strand=true. I saved the FASTA as NC_000005.10_hChrom5_TERT_CpG_Start.fasta. 

#### Analyzing the Alleged CpG Promoter Region
Dessain 2000 reported that the hTERT CpG island has a GC content of 74% and a CG:GC ratio of 0.87. Is that what I get for the same region?!? I wrote code in R to get the GC content and CG:GC ratio of the hTERT CpG promoter region that I identified. I didn't comment my code ... I am sorry. Note that I picked i=1164 cause Kumakura 2005 says that the hTERT CpG island to be from 654 bp upstream to 510 bp downstream of the ATG start codon, which is 654 + 510 = 1164 :) Here's R code that I didn't bother commenting :( 

```r
dna_file <- read.fasta("/media/david/Linux/Introns_Exons_and_Promoters/hTERT_CpG_Island/NC_000005.10_hChrom5_TERT_CpG_Start.fasta")
individual_characters <- dna_file[[1]]
i <- 1
CG_count <- 0
GC_count <- 0
g_count <- 0
c_count <- 0
for (letter in individual_characters) {
  #print(letter)
  i <- i + 1
  if (letter == "g") {
    g_count <- g_count + 1
  }
  if (letter == "c") {
    c_count <- c_count + 1
  }
  if ((letter == "c") & (last_letter == "g")) {
    GC_count <- GC_count + 1
  }
  if ((letter == "g") & (last_letter == "c")) {
    CG_count <- CG_count + 1
  }
  last_letter <- letter
  if (i >= 1164) {
    break
  }
}
print(100*(c_count+g_count)/1164)
print(GC_count)
print(CG_count)
print(CG_count/GC_count)
```
The lazily unlabeled output is:

[1] 76.03093
[1] 167
[1] 141
[1] 0.8443114

Cool-ness! My GC content is 76 % and the ratio of CpG/GpC is 0.84. Recall that Dessain 2000 reported that the hTERT CpG island has a GC content of 74% and a CG:GC ratio of 0.87. I'm 2 % off of the GC content and 0.03 off of the CpG/GpC. THAT'S PRETTY GOOD FOR REPLICATING DATA FROM A PAPER THAT IS ALMOST TWO DECADES OLD :D But, what if that was just random luck? I re-ran that same R code on the region AFTER the CpG island and I got wildly different data. Here's that code (yes, I should've used a function; I am lazy, lol):

```r
dna_file <- read.fasta("/media/david/Linux/Introns_Exons_and_Promoters/hTERT_CpG_Island/NC_000005.10_hChrom5_TERT_CpG_Start.fasta")
individual_characters <- dna_file[[1]]
#individual_characters[5]
i <- 1164
CG_count <- 0
GC_count <- 0
g_count <- 0
c_count <- 0
for (letter in individual_characters) {
  if (i <1164) {
    next
  }
  #print(letter)
  i <- i + 1
  if (letter == "g") {
    g_count <- g_count + 1
  }
  if (letter == "c") {
    c_count <- c_count + 1
  }
  if ((letter == "c") & (last_letter == "g")) {
    GC_count <- GC_count + 1
  }
  if ((letter == "g") & (last_letter == "c")) {
    CG_count <- CG_count + 1
  }
  last_letter <- letter
  
  
  if (i >= 42476) {
    break
  }
}
print(100*(c_count+g_count)/41312)
print(GC_count)
print(CG_count)
print(CG_count/GC_count)
```

The lazily unlabeled output is:

[1] 58.55926
[1] 3047
[1] 1654
[1] 0.542829

My GC content is 58.5 % and the ratio of CpG/GpC is 0.54. Recall that Dessain 2000 reported that the hTERT CpG island has a GC content of 74% and a CG:GC ratio of 0.87. THE REGION THAT IS NOT A CpG ISLAND IS 15.5% off of the GC content and 0.33 off of the CpG/GpC. I could dig into this with more statistical rigor, but I think you get the idea. I'M EXCITED!!! This was a really cool biological programming exercise!!! :D

# STN1 Mutation Triggers ALT in Yeast
ADDED STUFF
Counter 1996 The roles of telomeres and telomerase in cell life span
Yeast also can undergo a cellular catastrophe
analogous to the crisis induced in transformed human cells by the loss of telomeric DNA. Disruption
of any one of the S. ceret'isiae genes EST1, KEMI,
or TCL1 (TER1 in K. lactus) results in a loss of
telomeric DNA at the rate of approximately ~ 3-5
bp/generation. This shortening is accompanied by a
gradual increase in cell and chromosome loss. By
approximately generation 100, most cells perish
[7,57,58,162].
Counter 1996 The roles of telomeres and telomerase in cell life span
ADDED STUFF


ALT is a recombination-based telomere maintenace mechanism used by some human cancers to maintain cellular immortality. ALT cells typically have widly long, heterogenous telomeres. The exact molecular mechanism involved in this pathway are unknown. Iyer 2005 found that a STN1 gene mutation can initiate ALT in the yeast Kluyveromyces lactis. These ALT-like yeast cells experience a rapid telomere shortening when WT STN1 is re-introduced (Iyer 2005). There aren't any neat figures in this paper to talk about, so I'm going to try to replicate the protein multiple sequence alignment from Iyer 2005 figure 4. STN1 is aligned from K. lactis S. cerevisiae (Sc) and Candida glabrata (Cgl).

![Yeast_Protein_Alignment](/Assets/Yeast_Protein_Alignment.jpg "Yeast_Protein_Alignment")

#### Obtaining STN1 From 3 Yeast Organisms
The paper states that the S. cerevisiae (Sc) and Candida glabrata (Cgl) GenBank accession numbers are P_38960 and XP_448655. HOWEVER, it wasn't that easy to find the sequences cause those accession numbers are from back in 2005. NCBI says "The following term was not found in Nucleotide: P_38960." The XP_448655 is here: https://www.ncbi.nlm.nih.gov/protein/XP_448655. I had trouble finding the sequence for K. lactis they were talking about. Here's the crazy search term that I used on NCBI:

and it's the only result (other than whole chromosome chunks) w/ this crazy search term I made:
(((stn1) NOT "Pyrenophora tritici-repentis"[porgn:__txid45151] NOT "Fusarium fujikuroi"[porgn:__txid5127] NOT "[Candida] glabrata"[porgn:__txid5478] NOT "Hortaea werneckii"[porgn:__txid91943] NOT "Saccharomyces cerevisiae"[porgn:__txid4932]) NOT "Metarhizium robertsii"[porgn:__txid568076] NOT "Fusarium sp. FIESC_5 CS3069"[porgn:__txid1318460] NOT "Fusarium pseudograminearum CS3487"[porgn:__txid1318458] NOT "Fusarium pseudograminearum CS3427"[porgn:__txid1318457] NOT "Fusarium pseudograminearum CS3220"[porgn:__txid1318456] NOT "Fonsecaea multimorphosa"[porgn:__txid979981] NOT "Cladophialophora immunda"[porgn:__txid569365] NOT "Aspergillus nidulans FGSC A4"[porgn:__txid227321] NOT "Candida viswanathii"[porgn:__txid5486] NOT "Zygosaccharomyces bailii"[porgn:__txid4954] NOT "Metarhizium anisopliae"[porgn:__txid5530] NOT "Aspergillus flavus"[porgn:__txid5059] NOT "Talaromyces atroroseus"[porgn:__txid1441469] NOT "[Candida] auris"[porgn:__txid498019] NOT "Zygosaccharomyces rouxii"[porgn:__txid4956] NOT "[Candida] boidinii"[porgn:__txid5477] NOT "Komagataella phaffii"[porgn:__txid460519] NOT "Aspergillus fumigatus"[porgn:__txid746128] NOT "Candida albicans SC5314"[porgn:__txid237561] NOT "Yarrowia lipolytica"[porgn:__txid4952]) AND "Kluyveromyces lactis"[porgn:__txid28985] 

... I'm pretty sure that it's NCBI Reference Sequence: XM_452728.1, titled "Kluyveromyces lactis uncharacterized protein (KLLA0_C11825g), partial mRNA" BECAUSE that entry has this note "cerevisiae YDR082W STN1 Protein involved in telomere length regulation functions in telomere metabolism during late S phase." S. ceriviasa yeast was easier to find cause it's got stn1p in the title :) https://www.ncbi.nlm.nih.gov/nuccore/NM_001180390.1
                     
#### Attempt to Replicate Lyer 2005 Figure 4
I used the R msa library to align the three yeast organism STN1 proteins that were obtained above. I'm not too happy with this alignment :( The authors state that "The protein
sequences were aligned in ClustalW using default values." HOWEVER, the R msa package that I used was set to use ClustalW default values and it didn't replicate Figure 4 from Lyer 2005. The protein sequences seem to match (at least by eye). I'm not really sure where I went wrong here. I've only played with sequence alignment a little bit, so I'm probably doing something wrong. Anyway, here's the code:

```r
setwd("/media/david/Linux/Introns_Exons_and_Promoters/Yeast_STN1_ALT/Proteins")

library(msa)
All_Yeast_STN1_Protein <- "All_Yeast_STN1_Protein.fasta"
All_Yeast_STN1_Protein <- readDNAStringSet(All_Yeast_STN1_Protein)
All_Yeast_STN1_Protein_alignment <- msa(All_Yeast_STN1_Protein)
All_Yeast_STN1_Protein_alignment
msaPrettyPrint(All_Yeast_STN1_Protein_alignment, output="pdf", showNames="none",
showLogo="none", askForOverwrite=FALSE, verbose=FALSE)
```

![Aligning_Yeast_STN1_Proteins](/Assets/Aligning_Yeast_STN1_Proteins.jpg "Aligning_Yeast_STN1_Proteins")


#### Aligning Human, Yeast, and Frog STN1
Cohen 2002 reported that Xenopus laevis form extrachromosomal circular telomeric DNA. This is commonly associated with ALT! I briefly looked around for reptile ALT and this is the closest thing I could find. I'm not convinced that the activity reported by Cohen 2002 was actually ALT. This alignment isn't really related to anything. I just made it mostly for fun ... well, it's kinda connected to ALT and I know a herpetologist that might enjoy seeing frogs getting included in this repo ;) 

Cohen 2002 Formation of extrachromosomal circles from telomeric DNA in Xenopus laevis 
```r
Klactis_Xenopus_Human_STN1_Proteins <- "Klactis_Xenopus_Human_STN1_Proteins.fasta"
Klactis_Xenopus_Human_STN1_Proteins_AA <- readAAStringSet(Klactis_Xenopus_Human_STN1_Proteins)
Klactis_Xenopus_Human_STN1_Proteins_AA_alignment <- msa(Klactis_Xenopus_Human_STN1_Proteins_AA)
Klactis_Xenopus_Human_STN1_Proteins_AA_alignment
msaPrettyPrint(Klactis_Xenopus_Human_STN1_Proteins_AA_alignment, output="pdf", showNames="none",
showLogo="none", askForOverwrite=FALSE, verbose=FALSE)
```
![Klactis_Xenopus_Human_STN1_Proteins_AA_alignment](/Assets/Klactis_Xenopus_Human_STN1_Proteins_AA_alignment.jpg "Klactis_Xenopus_Human_STN1_Proteins_AA_alignment")

#### Mutant TP53 and ALT
Chen Association of Mutant TP53 with Alternative Lengthenig of telomre sand favorable prognosis in glioma
2006

#### ALT cells have Increased TERRA
each TERRA molecule comprises a chromosome-specific 5′ end followed by a tract of UUAGGG repeats, the length of which is proportional to telomere length (12)
Episkopou 2014 Alternative Lengthening of Telomeres is characterized by reduced compaction of telomeric chromatin
12 is
Arnoult N, Van Beneden A, Decottignies A. Telomere length regulates TERRA levels through increased trimethylation of telomeric H3K9 and HP1α Nat. Struct. Mol. Biol. 2012;19:948–956. 


#### Interesting Experimental Ideas
IMR90 SV40 parental of SW39 TEL+ and SW26 ALT+ SW13 ALT+
SW39 TEL+ was TERC KO went through crisis to become SW39 ALT+
Min 2017
ALT , TEL fusions some ALT some TEL ... what is the differential gene expression?

# Citations
* Cheng 2012 Caenorhabditis elegans POT-2 telomere protein represses a mode of alternative lengthening of telomeres with normal telomere lengths
* Cong 1999 The human telomerase catalytic subunit hTERT: organization of the gene and characterization of the promoter
* Lovejoy 2012 PLoS Genet Loss of ATRX, genome instability, altered DNA damage response hallmarks of ALT pathway
* Clynes 2013 Curr Opin Genet Dev ATRX and the replication of structured DNA
* Gonzalo 2006 DNA methyltransferases control telomere length and telomere recombination in mammalian cells.pdf
* Atkinson 2005 Lack of Telomerase Gene Expression in Alternative Lengthening of Telomere Cells Is Associated with Chromatin Remodeling of the hTR and hTERT Gene Promoters
* Kumakura 2005 Reversible Conversion of Immortal Human Cells from Telomerase-Positive to Telomerase-Negative Cells
* Cong 1999 The human telomerase catalytic subunit hTERT: organization of the gene and characterization of the promoter
* Dessain 2000 Methylation of the Human Telomerase Gene CpG Island
* Cheng 2012 Caenorhabditis elegans POT-2 telomere protein represses a mode of alternative lengthening of telomeres with normal telomere lengths
* Boeck 2016 The time resolved transcriptome of C. elegans
* Iyer 2005 A Mutation in the STN1 Gene Triggers an Alternative Lengthening of Telomere-Like Runaway Recombinational Telomere Elongation and Rapid Deletion in Yeast
* Cohen 2002 Formation of extrachromosomal circles from telomeric DNA in Xenopus laevis 
* Hu 2017 Imetelstat, a Telomerase Inhibitor, Is Capable of Depleting Myelofibrosis Hematopoietic Stem Cells and Progenitor Cells
* Weissman 2001 Telomere Shortening Accompanies Increased Cell Cycle Activity during Serial Transplantation of Hematopoietic Stem Cells
* Cesare 2010 Alternative lengthening of telomeres: models, mechanisms and implications
* Shay 2012 Cancer and Telomeres −− An ALTernative to Telomerase
* Harley 2008 Telomerase and cancer therapeutics
* Sahin 2012 Antitelomerase therapy provokes ALT and mitochondrial adaptive mechanisms in cancer
* Gocha 2013 Human Sarcomas Are Mosaic for Telomerase-Dependent and Telomerase-Independent Telomere Maintenance Mechanisms
* Kalmbach 2014 Telomere Length Reprogramming in Embryos and Stem Cells
* Huang 2014 Telomere regulation in pluripotent stem cells
* Dagg 2017 Extensive Proliferation of Human Cancer Cells with Ever-Shorter Telomeres
* Suda 2002 Interchromosomal Telomere Length Variation
* Cristofari 2006 Telomere length homeostasis requires that telomerase levels are limiting
* Gavory 2002 Minimum length requirement of the alignment domain of human telomerase RNA to sustain catalytic activity in vitro
* Murnane 1994 Telomere dynamics in an immortal human cell line
* Telomere elongation in immortal human cells without detectable telomerase activity


