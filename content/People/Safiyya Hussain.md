---
NID: Safiyya Hussain (1964)
Given Name: Safiyya
Last Name: Hussain
aliases:
DOB: 1964-07-13
DOD:
Gender: Female
Father: Hussain Naeem (1939)
Mother: Shaziyya Mohamed Didi (1948)
Blood Group: B+
Spouse 1: "[[Afzal Dad]]"
Spouse 2: "[[People/Family/Noora Family/Hawwa & Sitti Mom/Sihthy Faan/Hussain Thakhkhaan/Wife 1/Mohamed Hussain/Mohamed Hussain|Mohamed Hussain]]"
Spouse 2 Anniversary:
Spouse 2 Kids:
  - "[[Noora Mohamed]]"
  - "[[Hussain Noor Mohamed]]"
Spouse 2 Divorce: 2002-06-02
Phone Numbers:
  - "+9607607485"
E-mails:
  - safiyya.hussain64@gmail.com
Address:
  - "[[Likagasdhoshuge, Hithadhoo, Addu City, Maldives]]"
Type: Person
tags:
  - Dhonbeefaan/HawwaFaan/AminathManikfaan/ShaziyyaMohamedDidi/SafiyyaHussain
  - Hoabeyya/MohamedDidi/ShaziyyaMohamedDidi/SafiyyaHussain
  - AliKatheebThakurufaan/BoduMuhummadThakurufaan/HawwaFaan/AminathManikfaan/ShaziyyaMohamedDidi/SafiyyaHussain
  - Athiragey/KudhuRanaa/MariyamManikfaan/MoosaThahkhaan/AminathManikfaan/ShaziyyaMohamedDidi/SafiyyaHussain
  - AliKatheebThakurufaan/BoduMuakurufaan/HawwaFaan/AishathManikfaan/HussainNaeem/SafiyyaHussain
  - Athiragey/KudhuRanaa/MariyamManikfaan/MoosaThahkhaan/AishathManikfaan/HussainNaeem/SafiyyaHussain
  - Koshidhoragey/AdamThakurufaan/MoosaThahkhaan/HussainNaeem/SafiyyaHussain
Photo: https://lh3.googleusercontent.com/pw/AP1GczN3ReNeUKcRGaCAMU7xmtlzdgHQ0MHRXQAlwG-AyZ1-bA1nh01sowZVcXcbUwKnZ-ySGC5oFaWh9_-YwHS6Pqbxsib85Mi5UZinGZIe1KkwFjF0LbkibLT0-3W_H34Qfr1q5sDVjvqee0q9EEgMurQ=w768-h959-s-no?authuser=4
First Name:
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
