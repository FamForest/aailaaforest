---
NID: Hussain Noor Mohamed (1998)
First Name: Hussain
Given Name: Noor
Last Name: Mohamed
aliases:
  - Hussain Noor Mohamed
DOB: 1998-04-03
DOD:
Gender: Male
Father: Mohamed Hussain (1951)
Mother: Safiyya Hussain (1964)
Blood Group: B+
Spouse 1:
Spouse 1 Anniversary:
Spouse 1 Kids:
Spouse 1 Divorce:
Phone Numbers:
  - "+9609162587"
E-mails: noor.xbyte@gmail.com
Address:
  - "[[Likagasdhoshuge, Hithadhoo, Addu City, Maldives]]"
BML Accounts:
MIB Account:
Type: Person
tags:
  - Dhonbeefaan/HawwaFaan/AminathManikfaan/ShaziyyaMohamedDidi/SafiyyaHussain
  - Hoabeyya/MohamedDidi/ShaziyyaMohamedDidi/SafiyyaHussain
  - AliKatheebThakurufaan/BoduMuhummadThakurufaan/HawwaFaan/AminathManikfaan/ShaziyyaMohamedDidi/SafiyyaHussain
  - Athiragey/KudhuRanaa/MariyamManikfaan/MoosaThahkhaan/AminathManikfaan/ShaziyyaMohamedDidi/SafiyyaHussain
  - AliKatheebThakurufaan/BoduMuakurufaan/HawwaFaan/AishathManikfaan/HussainNaeem/SafiyyaHussain
  - Athiragey/KudhuRanaa/MariyamManikfaan/MoosaThahkhaan/AishathManikfaan/HussainNaeem/SafiyyaHussain
  - Koshidhoragey/AdamThakurufaan/MoosaThahkhaan/HussainNaeem/SafiyyaHussain
  - Dhonbeefaan/SihthyFaan/HussainThahkhaan/MohamedHussain
  - AliKatheebThakurufaan/BoduMuhummadThakurufaan/SihthyFaan/HussainThahkhaan/MohamedHussain
  - IsdhooSultanAli/SultanHassan/AliManikfaan/BandeyriHassanManikfaan/IbrahimManikfaan/GanduvaruDhonRahaa/HawwaDidi/HussainDidi/HassanDidi/Khadheeja/MohamedHussain
  - Munna/AmeerIbrahimFamuladheyriKilegefaanu/MoosaDidi/MaradhooAminaDidi/HawwaDidi/HussainDidi/HassanDidi/Khadheeja/MohamedHussain
  - Munna/IsdhooSultanIbrahimMuzhiruddin/MohamedManikfaan/AisaaManikfaan/MariyamManikfaan/MoosaDidi/Kuhdhihi/HawwaDidi/HussainDidi/HassanDidi/Khadheeja/MohamedHussain
  - Munna/MaradhooDhariMaigeyAhmedKoyya/Hassan/AminaManike/Khadheeja/MohamedHussain
  - IsdhooSultanAli/SultanHassan/IbrahimManikfaan/AishathManikfaan/IbrahimManikfaan/GanduvaruDhonRahaa/HawwaDidi/HussainDidi/HassanDidi/Khadheeja/MohamedHussain
Photo:
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
      formula.Photo: 106
      file.name: 141
      note.DOB: 105
      note.DOD: 105
      formula.Grand Mothers: 110
      formula.Grand Fathers: 110
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
      formula.Photo: 98
      file.name: 199
      formula.Gender: 90
      note.DOB: 115
    rowHeight: tall

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
      formula.Photo: 98
      file.name: 160
      note.DOB: 112
      formula.Mother: 139
      formula.Father: 139
    rowHeight: tall

```
