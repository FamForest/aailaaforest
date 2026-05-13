---
NID: Afeefa Hussain (1968)
First Name:
Given Name: Afeefa
Last Name: Hussain
aliases:
DOB: 1968-01-18
DOD:
Gender: Female
Father: Hussain Naeem (1939)
Mother: Shaziyya Mohamed Didi (1948)
Blood Group: B+
Spouse 1:
Spouse 1 Anniversary:
Phone Numbers:
  - "+9607613162"
E-mails:
Address:
  - "[[Likagasdhoshuge, Hithadhoo, Addu City, Maldives]]"
BML Accounts:
MIB Account:
Type: Person
tags:
  - Dhonbeefaan/HawwaFaan/AminathManikfaan/ShaziyyaMohamedDidi
  - Hoabeyya/MohamedDidi/ShaziyyaMohamedDidi
  - AliKatheebThakurufaan/BoduMuhummadThakurufaan/HawwaFaan/AminathManikfaan/ShaziyyaMohamedDidi
  - AliKatheebThakurufaan/BoduMuakurufaan/HawwaFaan/AishathManikfaan/HussainNaeem
  - Koshidhoragey/AdamThakurufaan/MoosaThahkhaan/HussainNaeem
  - Athiragey/KudhuRanaa/MariyamManikfaan/MoosaThahkhaan/AminathManikfaan/ShaziyyaMohamedDidi
  - Athiragey/KudhuRanaa/MariyamManikfaan/MoosaThahkhaan/AishathManikfaan/HussainNaeem
Photo: https://lh3.googleusercontent.com/pw/AP1GczN8bDruELAq5SIfa_CGI0SAT3ySCHoBxgb0BsuDwKsi8y7Vsa09Ow0fGF_dERrQZj7Gae3d1acUMgKoOQGiYUVMaU37UMvAHYzCYYsCz67P_gJXKEsy7M357ZeFfNeyCUM_d-7cfTh3c2ByMWP7N0s=w767-h959-s-no?authuser=4
Spouse 1 Kids:
publish: true
---
# About `= this.file.name`

**Full Name:** `= this.file.name`
**Gender:** `= this.gender`
**Status:** `= choice(this.DOD, "Deceased", "Living")`
**Date of Birth:** `= this.dob`
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
      file.name: 119
      note.DOB: 105
      note.DOD: 105
      formula.Grand Mothers: 129
      formula.Grand Fathers: 122
    rowHeight: tall
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
      note.DOB: 105
      note.DOD: 105
      formula.Grand Mothers: 158
      formula.Grand Fathers: 110

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
      formula.Photo: 105
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
