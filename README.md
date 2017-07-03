# SpringBoard-project1

Synopsis:

This project was created by springboard in order to help students, like myself, work on json files through the the python libarry, pandas. The project itself was composed of three excercises. While, the first two tested the basics of the promt, the last one was far more complicated.

Project:

JSON exercise¶

Using data in file 'data/world_bank_projects.json' and the techniques demonstrated above,

Find the 10 countries with most projects

Find the top 10 major project themes (using column 'mjtheme_namecode')

In 2. above you will notice that some entries have only the code and the name is missing. Create a dataframe with the missing names filled in.

IN[87]

json_df = pd.read_json('data/world_bank_projects.json')

json_df

#load as python data frame

IN[88]

answer1=json_df["countryname"].value_counts().head(10)

answer1 # Africa is not a country but a continent so I will need to drop it

answer1=answer1.drop("Africa")

answer1

Out[88]:

People's Republic of China         19

Republic of Indonesia              19

Socialist Republic of Vietnam      17

Republic of India                  16

Republic of Yemen                  13

Kingdom of Morocco                 12

People's Republic of Bangladesh    12

Nepal                              12

Republic of Mozambique             11

Name: countryname, dtype: int64

IN [89]

json_read=json.load(open("data/world_bank_projects.json"))#Load as a string

json_read=json_normalize(json_read,"mjtheme_namecode")

json_read["name"].value_counts().head(10) #However I see there is a blank space

Out [89]

Environment and natural resources management    223

Rural development                               202

Human development                               197

Public sector governance                        184

Social protection and risk management           158

Financial and private sector development        130

                                                122
																								
Social dev/gender/inclusion                     119

Trade and integration                            72

Urban development                                47

Name: name, dtype: int64

IN [90]

j=json_read #renamed database

#Created new dict with the codes as the keys of the dictionaries, and the name of the categories as the values

new_dict={}

for index in range(len(j)):

    if j.name[index]!="":
		
        new_dict[j.code[index]]=j.name[index]
				
#Now I recreated the dataframe by giving a name to all the blank spaces, by using the dictionary I recently created

for index in range(len(j)):

    if j.name[index]=="":
		
        j.name[index]=new_dict[j.code[index]]
				
j.head(10)

Out [90]

code	name

0	8	Human development

1	11	Environment and natural resources management

2	1	Economic management

3	6	Social protection and risk management

4	5	Trade and integration

5	2	Public sector governance

6	11	Environment and natural resources management

7	6	Social protection and risk management

8	7	Social dev/gender/inclusion

9	7	Social dev/gender/inclusion

#Created By Juan M. 



