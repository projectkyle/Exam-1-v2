# Exam-1-v2



1. My hypothesis is that people in the Northeast and West with at least an associates degree will have higher vaccination rates compared to people in the Midwest and South with at least an associates degree.

#code for extracting Northeast values with associates degree or higher
attach(Household_Pulse_data)

northeast <- (Household_Pulse_data$REGION == "Northeast") & (Household_Pulse_data$RECVDVACC == "yes got vaxx") & (Household_Pulse_data$EEDUC == "assoc deg") or (Household_Pulse_data$EEDUC == "bach deg") or (Household_Pulse_data$EEDUC == "adv deg")
summary(northeast)
detach()

#code for extracting West values with associates degree or higher
attach(Household_Pulse_data)

West <- (Household_Pulse_data$REGION == "West") & (Household_Pulse_data$RECVDVACC == "yes got vaxx") & (Household_Pulse_data$EEDUC == "assoc deg") or (Household_Pulse_data$EEDUC == "bach deg") or (Household_Pulse_data$EEDUC == "adv deg")
summary(west)
detach()

#code for extracting Midwest values with associates degree or higher
attach(Household_Pulse_data)

midwest <- (Household_Pulse_data$REGION == "Midwest") & (Household_Pulse_data$RECVDVACC == "yes got vaxx") & (Household_Pulse_data$EEDUC == "assoc deg") or (Household_Pulse_data$EEDUC == "bach deg") or (Household_Pulse_data$EEDUC == "adv deg")
summary(midwest)
detach()

south <- (Household_Pulse_data$REGION == "South") & (Household_Pulse_data$RECVDVACC == "yes got vaxx") & (Household_Pulse_data$EEDUC == "assoc deg") or (Household_Pulse_data$EEDUC == "bach deg") or (Household_Pulse_data$EEDUC == "adv deg")
summary(south)
detach()

2. My hypothesis is that Male and Female will have similar vaccine rates, Transgender, NA, and other will have similar vaccine rates.

attach(Household_Pulse_data)

# male 
male <- (Household_Pulse_data$GENID_DESCRIBE == "male") & (Household_Pulse_data$RECVDVACC == "yes got vaxx")
summary(male)

   Mode   FALSE    TRUE 
logical   45252   23862 

attach(Household_Pulse_data)

male <- (Household_Pulse_data$GENID_DESCRIBE == "male") & (Household_Pulse_data$RECVDVACC != "yes got vaxx")
summary(male)

   Mode   FALSE    TRUE 
logical   66180    2934 

# 23862:2934 or 1:.12 ratio

#female

female <- (Household_Pulse_data$GENID_DESCRIBE == "female") & (Household_Pulse_data$RECVDVACC == "yes got vaxx")
summary(female)

Mode   FALSE    TRUE 
logical   33896   35218 

female <- (Household_Pulse_data$GENID_DESCRIBE == "female") & (Household_Pulse_data$RECVDVACC != "yes got vaxx")
summary(female)

   Mode   FALSE    TRUE 
logical   64069    5045 

# 35218:5045 or 1:.14 ratio

#transgender

transgender <- (Household_Pulse_data$GENID_DESCRIBE == "transgender") & (Household_Pulse_data$RECVDVACC == "yes got vaxx")
summary(transgender)

   Mode   FALSE    TRUE 
logical   68947     167 

transgender <- (Household_Pulse_data$GENID_DESCRIBE == "transgender") & (Household_Pulse_data$RECVDVACC != "yes got vaxx")
summary(transgender)

   Mode   FALSE    TRUE 
logical   69079      35 

# 167:35 or 1:.21

#NA

NA <- (Household_Pulse_data$GENID_DESCRIBE == "NA") & (Household_Pulse_data$RECVDVACC != "yes got vaxx")
summary(NA)

Mode    NA's 
logical       1 

#other

other <- (Household_Pulse_data$GENID_DESCRIBE == "other") & (Household_Pulse_data$RECVDVACC == "yes got vaxx")
summary(other)

   Mode   FALSE    TRUE 
logical   68540     574 

other <- (Household_Pulse_data$GENID_DESCRIBE == "other") & (Household_Pulse_data$RECVDVACC != "yes got vaxx")
summary(other)

   Mode   FALSE    TRUE 
logical   68966     148 

# 574:148 or 1:.26

# The male and female ratio of vaxxed to not vaxxed are relatively similar. NA is inconclusive since there is only one person in the dataset labelled as NA, but between transgender and other, the vaccine rates are shown to be similar as well. It seems like both transgender and other are less inclined to get a vaccine compared to male or female.



3.
(80 points) Now do your own analysis using “Household_Pulse_data.RData”. Choose an interesting topic to explore, different from previous questions. The data includes information on housing (rent or own; whether behind on rent or mortgage), food shortage, whether work remote or in person, whether kids are in school in person or remote or homeschooled, how anxious or worried, vaxx status and plans, along with demographics like race/ethnicity, gender, marital status, and household income (as a factor). Choose a subgroup of the sample to consider and provide summary statistics of that subgroup. Explain why this subgroup is interesting. Form a hypothesis test about an interesting variable, explore whether your chosen subgroup differs from the rest of sample. Please provide both a p-value for the hypothesis test and a confidence interval. Write a short paragraph explaining the test (carefully noting what is the null hypothesis) and explaining the results of that test. Using a k-nn classifier, can you find relevant information to predict an interesting outcome? How good is the classifier? Discuss. Can you explain some other interesting information about this data? Some interesting crosstabs? Maybe regressions? Impress me.

The subgroup I will use will be those who have had anxiety or worries. Mental health has come into the spotlight since covid almost as much as physical health and it could be interesting to see how each gender responds to their mental well being.
The hypothesis is that women may be more likely to experience anxiety and worry. Women may also be more likely to work remotely since stereotypically, women are more likely to watch over children.
#code for summarizing data for those who did experienced anxiety and worry

attach(Household_Pulse_data)

anx_wor <- subset(Household_Pulse_data, (Household_Pulse_data$ANXIOUS != 'no anxiety over past 2 wks') & (Household_Pulse_data$WORRY != 'no worry over past 2 wks'))

detach() attach(anx_wor) summary(anx_wor)

#and here's the output

    RHISPANIC       RRACE                EEDUC              MS        EGENID_BIRTH  
Not Hispanic:31660 White:28772 less than hs: 250 NA : 687 male :11724
Hispanic : 3916 Black: 3052 some hs : 611 married :18701 female:23852
Asian: 1763 HS diploma :4309 widowed : 1646
Other: 1989 some coll :8271 divorced : 5737
assoc deg :4141 separated: 824
bach deg :9968 never : 7981
adv deg :8026
GENID_DESCRIBE SEXUAL_ORIENTATION KIDS_LT5Y
NA : 838 NA : 1027 NA :31445
male :11196 gay or lesbian: 1416 Yes children under 5 in HH: 4131
female :22886 straight :30171
transgender: 166 bisexual : 1735
other : 490 something else: 643
dont know : 584

                 KIDS_5_11Y                        KIDS_12_17Y   
NA :29005 NA :28976
Yes children 5 - 11 in HH: 6571 Yes children 12 - 17 in HH: 6600

                          ENROLLNONE                  RECVDVACC                          DOSESRV     
NA :32795 NA : 717 NA : 5418
children not in any type of school: 2781 yes got vaxx :30350 yes got all doses :28810
no did not get vaxx: 4509 yes plan to get all doses: 1189
no will not get all doses: 159

                 GETVACRV                                   KIDDOSES    
NA :31105 NA :29200
definitely will get vaxx: 409 Yes kids got or will get all doses: 4186
probably will get vaxx : 445 no kids did not or will not : 2190
unsure about vaxx : 994
probably not : 852
definitely not : 1771

                KIDGETVAC                          HADCOVID                      WRKLOSSRV    
NA :33354 NA : 1233 NA : 1893
definitely will get vaxx: 312 yes doctor told had covid: 5151 yes recent HH job loss: 5971
probably will get vaxx : 261 no did not :28927 no recent HH job loss :27712
unsure about vaxx : 463 not sure : 265
probably not : 341
definitely not : 568
dont know yet : 277
ANYWORK KINDWORK RSNNOWRKRV
NA : 1998 NA :15767 NA :23308
yes employment in last 7 days:20272 work for govt : 3298 retired : 4610
no employment in last 7 days :13306 work for private co:10993 other : 2457
work for nonprofit : 2690 sick or disabled: 1100
self employed : 2425 caring for kids : 901
work in family biz : 403 laid off : 884
(Other) : 2316
CHLDCARE CURFOODSUF
NA :29145 NA : 6640
yes impacts to childcare because pandemic: 1995 had enough food :19117
no : 4436 had enough but not what wanted: 7168
sometimes not enough food : 2073
often not enough food : 578

                                           CHILDFOOD    
NA :31867
often kids not eating enough because couldnt afford: 230
sometimes kids not eating enough : 999
kids got enough food : 2480

                                        ANXIOUS     
NA : 7924
no anxiety over past 2 wks : 0
several days anxiety over past 2 wks :13547
more than half the days anxiety over past 2 wks: 5707
nearly every day anxiety : 8398

                                         WORRY                                 TENURE     
NA : 7943 NA : 9327
no worry over past 2 wks : 0 housing owned free and clear : 5546
several days worried over past 2 wks :16564 housing owned with mortgage :12851
more than half the days worried over past 2 wks: 4868 housing rented : 7437
nearly every day worry : 6201 housing occupied without rent: 415

                            LIVQTRRV                RENTCUR                     MORTCUR     
live in detached 1 family :17652 NA :28158 NA :22772
NA : 9416 current on rent: 6436 current on mortgage:11841
live in bldg w 5+ apts : 3589 behind on rent : 982 behind on mortgage : 963
live in 1 family attached to others: 2148
live in building with 3-4 apts : 975
live in mobile home : 933
(Other) : 863
EVICT FORCLOSE
NA :34619 NA :34628
very likely evicted in next 2 months : 178 very likely forclosed in next 2 months : 48
somewhat likely evicted in next 2 months : 327 somewhat likely forclosed in next 2 months : 179
not very likely evicted in next 2 months : 266 not very likely forclosed in next 2 months : 369
not at all likely evicted in next 2 months: 186 not at all forclosed evicted in next 2 months: 352

       EST_ST                        PRIVHLTH                      PUBHLTH            REGION     
California : 2841 has private health ins:20659 has public health ins: 9363 Northeast: 5331
Texas : 1976 no private health ins : 5783 no public health ins :16327 South :11871
Florida : 1389 NA : 9134 NA : 9886 Midwest : 6754
Washington : 1372 West :11620
Oregon : 1070
Massachusetts: 985
(Other) :25943
INCOME Num_kids_Pub_School Num_kids_Priv_School Num_kids_homeschool NA :14352 Min. :0.000 Min. :0.00 Min. :0.00
HH income $35k - 49.9 : 4353 1st Qu.:1.000 1st Qu.:0.00 1st Qu.:0.00
HH income $75 - 99.9 : 4035 Median :2.000 Median :1.00 Median :1.00
HH income $50k - 74.9 : 3389 Mean :1.713 Mean :0.98 Mean :0.87
HH income $25k - $34.9k : 3051 3rd Qu.:2.000 3rd Qu.:2.00 3rd Qu.:2.00
HH income less than $25k: 2516 Max. :4.000 Max. :2.00 Max. :2.00
(Other) : 3880 NA's :27133 NA's :34027 NA's :34514
Works_onsite works_remote Shop_in_store eat_in_restaurant NA : 5664 NA : 6333 NA : 5954 NA : 6100
worked onsite:17609 worked remotely:11318 shopped in store:24882 eat at restaurant indoors:13386
no :12303 no :17925 no : 4740 no :16090

code for men experiencing worry and anxiety

men_anx_wor <- subset(Household_Pulse_data, (Household_Pulse_data$ANXIOUS != 'no anxiety over past 2 wks') & (Household_Pulse_data$WORRY != 'no worry over past 2 wks') & (EGENID_BIRTH == 'male')) summary(men_anx_wor)

output

   RHISPANIC       RRACE               EEDUC              MS       EGENID_BIRTH       GENID_DESCRIBE 
Not Hispanic:10351 White:9436 less than hs: 100 NA : 253 male :11724 NA : 332
Hispanic : 1373 Black: 854 some hs : 232 married :6687 female: 0 male :11141
Asian: 742 HS diploma :1420 widowed : 293 female : 43
Other: 692 some coll :2777 divorced :1463 transgender: 54
assoc deg :1142 separated: 219 other : 154
bach deg :3390 never :2809
adv deg :2663
SEXUAL_ORIENTATION KIDS_LT5Y KIDS_5_11Y
NA : 378 NA :10477 NA :9824
gay or lesbian: 790 Yes children under 5 in HH: 1247 Yes children 5 - 11 in HH:1900
straight :9802
bisexual : 341
something else: 189
dont know : 224

                 KIDS_12_17Y                                ENROLLNONE                  RECVDVACC    
NA :9802 NA :10832 NA : 259
Yes children 12 - 17 in HH:1922 children not in any type of school: 892 yes got vaxx :10069
no did not get vaxx: 1396

                  DOSESRV                         GETVACRV    
NA :1719 NA :10334
yes got all doses :9620 definitely will get vaxx: 122
yes plan to get all doses: 330 probably will get vaxx : 145
no will not get all doses: 55 unsure about vaxx : 247
probably not : 275
definitely not : 601

                           KIDDOSES                       KIDGETVAC    
NA :9888 NA :11111
Yes kids got or will get all doses:1249 definitely will get vaxx: 97
no kids did not or will not : 587 probably will get vaxx : 74
unsure about vaxx : 114
probably not : 101
definitely not : 154
dont know yet : 73
HADCOVID WRKLOSSRV ANYWORK
NA : 437 NA : 717 NA : 756
yes doctor told had covid:1609 yes recent HH job loss:2155 yes employment in last 7 days:6940
no did not :9563 no recent HH job loss :8852 no employment in last 7 days :4028
not sure : 115

            KINDWORK                        RSNNOWRKRV  
NA :4906 NA :8064
work for govt :1023 retired :1519
work for private co:4171 other : 689
work for nonprofit : 552 laid off : 347
self employed : 932 sick or disabled : 286
work in family biz : 140 concerned about spreading: 164
(Other) : 655
CHLDCARE CURFOODSUF
NA :9877 NA :2546
yes impacts to childcare because pandemic: 545 had enough food :6058
no :1302 had enough but not what wanted:2265
sometimes not enough food : 650
often not enough food : 205

                                           CHILDFOOD    
NA :10720
often kids not eating enough because couldnt afford: 76
sometimes kids not eating enough : 263
kids got enough food : 665

                                        ANXIOUS    
NA :3055
no anxiety over past 2 wks : 0
several days anxiety over past 2 wks :4443
more than half the days anxiety over past 2 wks:1739
nearly every day anxiety :2487

                                         WORRY                                TENURE    
NA :3060 NA :3514
no worry over past 2 wks : 0 housing owned free and clear :1798
several days worried over past 2 wks :5431 housing owned with mortgage :3985
more than half the days worried over past 2 wks:1428 housing rented :2276
nearly every day worry :1805 housing occupied without rent: 151

                            LIVQTRRV               RENTCUR                    MORTCUR    
live in detached 1 family :5475 NA :9457 NA :7758
NA :3562 current on rent:1988 current on mortgage:3666
live in bldg w 5+ apts :1201 behind on rent : 279 behind on mortgage : 300
live in 1 family attached to others: 627
live in building with 3-4 apts : 318
live in mobile home : 244
(Other) : 297
EVICT FORCLOSE
NA :11454 NA :11429
very likely evicted in next 2 months : 51 very likely forclosed in next 2 months : 19
somewhat likely evicted in next 2 months : 87 somewhat likely forclosed in next 2 months : 53
not very likely evicted in next 2 months : 78 not very likely forclosed in next 2 months : 119
not at all likely evicted in next 2 months: 54 not at all forclosed evicted in next 2 months: 104

    EST_ST                       PRIVHLTH                     PUBHLTH           REGION    
California:1055 has private health ins:6494 has public health ins:2900 Northeast:1748
Texas : 681 no private health ins :1789 no public health ins :5096 South :3811
Washington: 465 NA :3441 NA :3728 Midwest :2203
Florida : 446 West :3962
Utah : 327
Oregon : 322
(Other) :8428
INCOME Num_kids_Pub_School Num_kids_Priv_School Num_kids_homeschool NA :4902 Min. :0.00 Min. :0.000 Min. :0.000
HH income $75 - 99.9 :1351 1st Qu.:1.00 1st Qu.:1.000 1st Qu.:0.000
HH income $35k - 49.9 :1332 Median :2.00 Median :1.000 Median :1.000
HH income $50k - 74.9 :1064 Mean :1.72 Mean :1.071 Mean :0.933
HH income $25k - $34.9k: 904 3rd Qu.:2.00 3rd Qu.:2.000 3rd Qu.:2.000
HH income $150 - 199 : 798 Max. :4.00 Max. :2.000 Max. :2.000
(Other) :1373 NA's :9323 NA's :11229 NA's :11409
Works_onsite works_remote Shop_in_store eat_in_restaurant NA :2141 NA :2361 NA :2252 NA :2289
worked onsite:5476 worked remotely:3883 shopped in store:8054 eat at restaurant indoors:4645
no :4107 no :5480 no :1418 no :4790

code for women experiencing worry and anxiety

women_anx_wor <- subset(Household_Pulse_data, (Household_Pulse_data$ANXIOUS != 'no anxiety over past 2 wks') & (Household_Pulse_data$WORRY != 'no worry over past 2 wks') & (EGENID_BIRTH == 'female')) summary(men_anx_wor)

#output

    RHISPANIC       RRACE               EEDUC              MS       EGENID_BIRTH       GENID_DESCRIBE 
Not Hispanic:10351 White:9436 less than hs: 100 NA : 253 male :11724 NA : 332
Hispanic : 1373 Black: 854 some hs : 232 married :6687 female: 0 male :11141
Asian: 742 HS diploma :1420 widowed : 293 female : 43
Other: 692 some coll :2777 divorced :1463 transgender: 54
assoc deg :1142 separated: 219 other : 154
bach deg :3390 never :2809
adv deg :2663
SEXUAL_ORIENTATION KIDS_LT5Y KIDS_5_11Y
NA : 378 NA :10477 NA :9824
gay or lesbian: 790 Yes children under 5 in HH: 1247 Yes children 5 - 11 in HH:1900
straight :9802
bisexual : 341
something else: 189
dont know : 224

                 KIDS_12_17Y                                ENROLLNONE                  RECVDVACC    
NA :9802 NA :10832 NA : 259
Yes children 12 - 17 in HH:1922 children not in any type of school: 892 yes got vaxx :10069
no did not get vaxx: 1396

                  DOSESRV                         GETVACRV    
NA :1719 NA :10334
yes got all doses :9620 definitely will get vaxx: 122
yes plan to get all doses: 330 probably will get vaxx : 145
no will not get all doses: 55 unsure about vaxx : 247
probably not : 275
definitely not : 601

                           KIDDOSES                       KIDGETVAC    
NA :9888 NA :11111
Yes kids got or will get all doses:1249 definitely will get vaxx: 97
no kids did not or will not : 587 probably will get vaxx : 74
unsure about vaxx : 114
probably not : 101
definitely not : 154
dont know yet : 73
HADCOVID WRKLOSSRV ANYWORK
NA : 437 NA : 717 NA : 756
yes doctor told had covid:1609 yes recent HH job loss:2155 yes employment in last 7 days:6940
no did not :9563 no recent HH job loss :8852 no employment in last 7 days :4028
not sure : 115

            KINDWORK                        RSNNOWRKRV  
NA :4906 NA :8064
work for govt :1023 retired :1519
work for private co:4171 other : 689
work for nonprofit : 552 laid off : 347
self employed : 932 sick or disabled : 286
work in family biz : 140 concerned about spreading: 164
(Other) : 655
CHLDCARE CURFOODSUF
NA :9877 NA :2546
yes impacts to childcare because pandemic: 545 had enough food :6058
no :1302 had enough but not what wanted:2265
sometimes not enough food : 650
often not enough food : 205

                                           CHILDFOOD    
NA :10720
often kids not eating enough because couldnt afford: 76
sometimes kids not eating enough : 263
kids got enough food : 665

                                        ANXIOUS    
NA :3055
no anxiety over past 2 wks : 0
several days anxiety over past 2 wks :4443
more than half the days anxiety over past 2 wks:1739
nearly every day anxiety :2487

                                         WORRY                                TENURE    
NA :3060 NA :3514
no worry over past 2 wks : 0 housing owned free and clear :1798
several days worried over past 2 wks :5431 housing owned with mortgage :3985
more than half the days worried over past 2 wks:1428 housing rented :2276
nearly every day worry :1805 housing occupied without rent: 151

                            LIVQTRRV               RENTCUR                    MORTCUR    
live in detached 1 family :5475 NA :9457 NA :7758
NA :3562 current on rent:1988 current on mortgage:3666
live in bldg w 5+ apts :1201 behind on rent : 279 behind on mortgage : 300
live in 1 family attached to others: 627
live in building with 3-4 apts : 318
live in mobile home : 244
(Other) : 297
EVICT FORCLOSE
NA :11454 NA :11429
very likely evicted in next 2 months : 51 very likely forclosed in next 2 months : 19
somewhat likely evicted in next 2 months : 87 somewhat likely forclosed in next 2 months : 53
not very likely evicted in next 2 months : 78 not very likely forclosed in next 2 months : 119
not at all likely evicted in next 2 months: 54 not at all forclosed evicted in next 2 months: 104

    EST_ST                       PRIVHLTH                     PUBHLTH           REGION    
California:1055 has private health ins:6494 has public health ins:2900 Northeast:1748
Texas : 681 no private health ins :1789 no public health ins :5096 South :3811
Washington: 465 NA :3441 NA :3728 Midwest :2203
Florida : 446 West :3962
Utah : 327
Oregon : 322
(Other) :8428
INCOME Num_kids_Pub_School Num_kids_Priv_School Num_kids_homeschool NA :4902 Min. :0.00 Min. :0.000 Min. :0.000
HH income $75 - 99.9 :1351 1st Qu.:1.00 1st Qu.:1.000 1st Qu.:0.000
HH income $35k - 49.9 :1332 Median :2.00 Median :1.000 Median :1.000
HH income $50k - 74.9 :1064 Mean :1.72 Mean :1.071 Mean :0.933
HH income $25k - $34.9k: 904 3rd Qu.:2.00 3rd Qu.:2.000 3rd Qu.:2.000
HH income $150 - 199 : 798 Max. :4.00 Max. :2.000 Max. :2.000
(Other) :1373 NA's :9323 NA's :11229 NA's :11409
Works_onsite works_remote Shop_in_store eat_in_restaurant NA :2141 NA :2361 NA :2252 NA :2289
worked onsite:5476 worked remotely:3883 shopped in store:8054 eat at restaurant indoors:4645
no :4107 no :5480 no :1418 no :4790
