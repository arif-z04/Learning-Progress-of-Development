```mermaid
flowchart LR

    %% =========================
    %% ENTITIES
    %% =========================
    classDef entity stroke:#ee6b6e;

    USERS[USERS]:::entity

    ROLES[ROLES]:::entity

    USERROLES[USER ROLES]:::entity

    STAFF[STAFF PROFILES]:::entity

    PATIENTS[PATIENTS]:::entity

    DOCTORS[DOCTORS]:::entity

    AVAILABILITY[DOCTOR AVAILABILITY]:::entity

    APPOINTMENTS[APPOINTMENTS]:::entity

    SESSIONNOTES[SESSION NOTES]:::entity

    MEDICALREPORTS[MEDICAL REPORTS]:::entity

    PRODUCTS[PRODUCTS]:::entity

    CARTS[CARTS]:::entity

    CARTITEMS[CART ITEMS]:::entity

    ORDERS[ORDERS]:::entity

    ORDERITEMS[ORDER ITEMS]:::entity

    PAYMENTS[PAYMENTS]:::entity

    CHATROOMS[CHAT ROOMS]:::entity

    CHATMESSAGES[CHAT MESSAGES]:::entity

    NOTIFICATIONS[NOTIFICATIONS]:::entity

    AUDITLOGS[AUDIT LOGS]:::entity


    %% =========================
    %% RELATIONSHIPS
    %% =========================

    EXTENDS1{EXTENDS}
    EXTENDS2{EXTENDS}
    HASROLE{HAS ROLE}
    ASSIGNED{ASSIGNED BY}

    MANAGES{MANAGES}
    
    DEFINES{DEFINES}

    BOOKS{BOOKS}

    ATTENDS{ATTENDS}

    WRITES{WRITES}

    OWNS{OWNS}

    UPLOADS{UPLOADS}

    ADDS{ADDS}

    CONTAINS1{CONTAINS}

    CONTAINS2{CONTAINS}

    PLACES{PLACES}

    PAYS{PAYS}

    PARTICIPATES{PARTICIPATES}

    SENDS{SENDS}

    RECEIVES{RECEIVES}

    RECORDS{RECORDS}



    %% =========================
    %% USER MANAGEMENT
    %% =========================

    USERS -- "1" --- EXTENDS1
    EXTENDS1 -- "1" --- PATIENTS


    USERS -- "1" --- EXTENDS2
    EXTENDS2 -- "1" --- DOCTORS


    USERS -- "1" --- HASROLE
    HASROLE -- "Many" --- USERROLES


    ROLES -- "1" --- USERROLES


    USERS -- "1" --- STAFF
    STAFF -- "1" --- MANAGES



    %% =========================
    %% DOCTOR / PATIENT MODULE
    %% =========================

    DOCTORS -- "1" --- DEFINES
    DEFINES -- "Many" --- AVAILABILITY


    PATIENTS -- "1" --- BOOKS
    BOOKS -- "Many" --- APPOINTMENTS


    DOCTORS -- "1" --- ATTENDS
    ATTENDS -- "Many" --- APPOINTMENTS


    APPOINTMENTS -- "1" --- WRITES
    WRITES -- "0 or 1" --- SESSIONNOTES


    PATIENTS -- "1" --- OWNS
    OWNS -- "Many" --- MEDICALREPORTS


    USERS -- "1" --- UPLOADS
    UPLOADS -- "Many" --- MEDICALREPORTS



    %% =========================
    %% E-COMMERCE MODULE
    %% =========================

    USERS -- "1" --- OWNS
    OWNS -- "1" --- CARTS


    CARTS -- "1" --- CONTAINS1
    CONTAINS1 -- "Many" --- CARTITEMS


    PRODUCTS -- "1" --- ADDS
    ADDS -- "Many" --- CARTITEMS


    USERS -- "1" --- PLACES
    PLACES -- "Many" --- ORDERS


    ORDERS -- "1" --- CONTAINS2
    CONTAINS2 -- "Many" --- ORDERITEMS


    PRODUCTS -- "1" --- ADDS
    ADDS -- "Many" --- ORDERITEMS


    ORDERS -- "1" --- PAYS
    PAYS -- "0 or 1" --- PAYMENTS



    %% =========================
    %% CHAT MODULE
    %% =========================

    USERS -- "Many" --- PARTICIPATES
    PARTICIPATES -- "Many" --- CHATROOMS


    CHATROOMS -- "1" --- SENDS
    SENDS -- "Many" --- CHATMESSAGES


    USERS -- "1" --- SENDS
    SENDS -- "Many" --- CHATMESSAGES



    %% =========================
    %% SYSTEM MODULE
    %% =========================

    USERS -- "1" --- RECEIVES
    RECEIVES -- "Many" --- NOTIFICATIONS


    USERS -- "1" --- RECORDS
    RECORDS -- "Many" --- AUDITLOGS

```