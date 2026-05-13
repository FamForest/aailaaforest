---
NID: Hussain Naeem (1939)
Given Name: Hussain Naeem
Last Name:
aliases:
DOB: 1939-06-09
DOD: 2016-08-15
Gender: Male
Father: Moosa Thakhkhaan
Mother: Aishath Manikfaan
Blood Group: B-
Spouse 1: "[[Kadhdha Didi]]"
Spouse 2: "[[Shaziyya Mohamed Didi|Shaziyya Mohamed Didi]]"
Spouse 1 Kids:
  - "[[Fathmath Hussain]]"
Spouse 2 Kids:
  - "[[Safiyya Hussain]]"
  - "[[Afeefa Hussain]]"
  - "[[Azeeza Hussain]]"
Phone Numbers:
Address:
Type: Person
tags:
  - AliKatheebThakurufaan/BoduMuhummadThakurufaan/HawwaFaan/AishathManikfaan/HussainNaeem
  - Athiragey/KudhuRanaa/MariyamManikfaan/MoosaThahkhaan/AishathManikfaan/HussainNaeem
  - Koshidhoragey/AdamThakurufaan/MoosaThahkhaan/HussainNaeem
  - Nooraaneemaage
Photo: https://lh3.googleusercontent.com/pw/AP1GczOmuKisSZxW1xFXk8govWUqt2lRhQcpaHIylFEoTyE1Z_TJwfmq3XRxIjg8v0SFtymKxxnA5jq-EA0CPC0OHLJzOzLvPO1AZ3eZdu5s2MhttXwH_YqXMz1biyDIvwXKAEi1AE97ucNWk-Rcz5e0OQWf=w719-h959-s-no?authuser=0
publish: true
---
# About `= this.file.name`

**Full Name:** `= this.file.name`
**Gender:** `= this.gender`
**Status:** `= choice(this.DOD, "Passed " + (date(today) - date(this.DOD)) + " ago", "Living")`
**Date of Birth:** `= this.dob`
**Date of Death:** `= this.dod` 
**Age at Death:** `= this.dod - this.dob`
**Current Age:** `= date(today) - this.dob`


# Family Relationships

## `= this.given-name`'s Parents & Grandparents
```base
filters:
  and:
    - Type == "Person"
    - file.path.startsWith("People")
formulas:
  Photo: image(Photo)
  Grand Mothers: |
    Mother.split(" (",1)
  Grand Fathers: |
    Father.split(" (",1)
properties:
  note.Mother:
    displayName: Grand Mothers
  note.Father:
    displayName: Grand Fathers
  file.name:
    displayName: Parent's Name
views:
  - type: table
    name: Parents
    filters:
      or:
        - NID == this.Mother
        - NID == this.Father
    order:
      - file.name
      - DOB
      - DOD
      - formula.Grand Mothers
      - formula.Grand Fathers
    columnSize:
      file.name: 178
      note.DOB: 110
      note.DOD: 110
    indentProperties: true
  - type: table
    name: Parents Photo
    filters:
      or:
        - NID == this.Mother
        - NID == this.Father
    order:
      - formula.Photo
      - file.name
      - DOB
      - DOD
      - formula.Grand Mothers
      - formula.Grand Fathers
    columnSize:
      formula.Photo: 98
      file.name: 141
      note.DOB: 105
      note.DOD: 105
      formula.Grand Mothers: 110
      formula.Grand Fathers: 110
    rowHeight: tall

```

## `= this.given-name`'s Children by Spouse(s)
```base
filters:
  and:
    - Type == "Person"
    - file.path.startsWith("People")
formulas:
  Spouse: if(this.Gender.isEmpty(),"Select Gender of the Person You're Viewing",if(this.gender.contains("Female"),Father.split(" (",1),Mother.split(" (",1)))
  Gender: if(Gender.isEmpty(),"Child",if(Gender.contains("Female"),"Daughter","Son"))
  Photo: image(Photo)
properties:
  file.name:
    displayName: Child's Name
views:
  - type: table
    name: Children Photo
    filters:
      or:
        - Father == this.NID
        - Mother == this.NID
    order:
      - formula.Photo
      - file.name
      - formula.Gender
      - DOB
      - formula.Spouse
    sort:
      - property: DOB
        direction: ASC
    columnSize:
      formula.Photo: 105
      file.name: 199
      formula.Gender: 90
      note.DOB: 115
    rowHeight: tall
  - type: table
    name: Children
    filters:
      or:
        - Father == this.NID
        - Mother == this.NID
    order:
      - file.name
      - formula.Gender
      - DOB
      - formula.Spouse
    sort:
      - property: DOB
        direction: ASC
    columnSize:
      file.name: 241
      formula.Gender: 90
      note.DOB: 115

```

## `= this.given-name`'s Siblings & Half-siblings
```base
filters:
  and:
    - Type == "Person"
    - file.path.startsWith("People")
formulas:
  Gender: if(Gender.isEmpty(),"Sibling",if(gender.contains("Female"),"Sister","Brother"))
  Mother: Mother.split(" (",1)
  mother: mother.split(" (",1)
  Father: Father.split(" (",1)
  Photo: image(Photo)
properties:
  file.name:
    displayName: Sibling's Name
  formula.Father:
    displayName: Father
  formula.Mother:
    displayName: Mother
views:
  - type: table
    name: Siblings and Half Siblings
    filters:
      and:
        - NID != this.NID
        - or:
            - Father == this.Father
            - Mother == this.Mother
    order:
      - formula.Photo
      - file.name
      - formula.Gender
      - DOB
      - formula.Mother
      - formula.Father
    sort:
      - property: Mother
        direction: ASC
    columnSize:
      formula.Photo: 108
      file.name: 160
      note.DOB: 112
      formula.Mother: 139
      formula.Father: 139
    rowHeight: tall
  - type: table
    name: Siblings & Half Siblings
    filters:
      and:
        - NID != this.NID
        - or:
            - Father == this.Father
            - Mother == this.Mother
    order:
      - file.name
      - formula.Gender
      - DOB
      - formula.Mother
      - formula.Father
    sort:
      - property: DOB
        direction: ASC
    columnSize:
      note.DOB: 112
      formula.Father: 139
      formula.Mother: 139

```
