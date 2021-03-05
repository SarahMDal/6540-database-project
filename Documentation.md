# Schema documentation

Generated by MySQL Workbench Model Documentation v1.0.0 - Copyright (c) 2015 Hieu Le

## Table: `artists`

### Description: 

Artist name, location, genre, role/activities, contact info, social media links

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `artist_id` | INT | PRIMARY, Auto increments, Not null |   | primary key<br /><br />**foreign key** to column `artist_id` on table `artists`. |
| `artist_name` | VARCHAR(50) |  |   | name of artist as they are now. Do not use birth names - only names that the artist self-identifies with. |
| `contact_id` | INT |  |   | foreign key - non-social media contact info for artist - might be email or other means. If agent, use agents email and place agent company under artist_affiliations<br /><br />**foreign key** to column `contact_id` on table `contact_info`. |
| `social_id` | INT |  |   | Artist social media site, such as Twitter, FB, Soundcloud, Bandcamp, youtube, etc.<br /><br />**foreign key** to column `social_id` on table `social_media`. |
| `artist_active` | VARCHAR(10) |  |   | Is the artist currently active? Possible entries: Yes or No. |
| `archive_id` | INT | PRIMARY, Not null |   |   |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `artist_id`, `archive_id` | PRIMARY | Information pertaining to the artist including name, activity level, and IDs for associative social media and contact tables. This table is central to the associative tables linking artist's names to their genres, production, and global affiliations.<br /> |
| fk_social_id_idx | `social_id` | INDEX |   |
| fk_contact_id_idx | `contact_id` | INDEX |   |


## Table: `affiliations`

### Description: Information on affiliations. With a global view: clubs, residencies, festivals, record lables, agents, collectives, record shops, collaborations, radio stations that focus on electronic music. Artists may have many affiliations and over time, these will change. For example, its not uncommon for artists to change record labels as they increase popularity, or even start their own. Collaborations is a very common practice, so most will have several collaborations with other artists. 

This table is important to provide a historical view of the artist's journey and is not currently found on existing databases. 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `affil_id` | INT | PRIMARY, Not null |   | Primary key |
| `affil_type` | VARCHAR(100) |  |   | Type of affiliation (e.g. club, residency, record label, collaboration, agent, radio station) Please only enter one type per id. For example, a record label like Soma Records will be its own record as many artists may release albums with Soma. |
| `affil_name` | VARCHAR(100) |  |   | Name of the affiliation, such as listed on its website. For example, The Lot Radio uses a capital 'T'. This could include other artists names as well, though we should expect spelling variations. |
| `affil_city` | VARCHAR(100) |  |   | The city where the affiliation is located, such as New York or Berlin.<br />Use country when city is not well known. For example, Berlin is well known, but Sugar Mountain should have the country identifier, Australia, as it is less well known to a general audience.<br /> |
| `affil_url` | VARCHAR(200) |  |   | The affiliation’s website/social media URL. Please include the complete address so that the link can be made clickable without cleaning later.<br />Thank you!<br /> |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `affil_id` | PRIMARY | Information on affiliations. With a global view: clubs, residencies, festivals, record lables, agents, collectives, record shops, collaborations, radio stations that focus on electronic music. Artists may have many affiliations and over time, these will change. For example, its not uncommon for artists to change record labels as they increase popularity, or even start their own. Collaborations is a very common practice, so most will have several collaborations with other artists.<br /><br />This table is important to provide a historical view of the artist's journey and is not currently found on existing databases. |


## Table: `genre`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `genre_id` | INT | PRIMARY, Not null |   | primary key |
| `genre_name` | VARCHAR(80) | Not null |   | The name of the music genre. If possible, this should be identified by the set, track or album information from the source. This may include multiple styles that are merged. Sources might include from the artist' website or record label as well as tags from Soundcloud or Basecamp. There may be multiple strings together, such as UK hard house as an example. |
| `genre_description` | VARCHAR(100) |  |   | A description of the genre, can include general sound, feel, asthetic, important history. For example, an artist may produce trance tracks, but within a sound that is typical of Berlin. This is important as it helps connect sound with place that may be outside of an artist's geographic location. For example, many artists play a stripped down Detroit sound but do not live or play in Detroit. |
| `genre_notes` | VARCHAR(200) |  |   | Any other specific details that do not fit in the above, such as aspects of the sound that the artist claims is unique, the originator, references, etc.<br />This is important as it starts to contribute to a history of artists, genres and production. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `genre_id` | PRIMARY | Genre of music as identified by the artist.  Priority is to let artist self-identify and pull from their info, such as their website or distribution channel. Multiple styles likely for each artist.<br />This table mimics other databases with artists organized by genre to aid in discovery.<br /> |


## Table: `artist_self`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `artist_id` | INT | PRIMARY, Not null |   |  **foreign key** to column `artist_id` on table `artists`. |
| `self_id` | INT | PRIMARY, Not null |   |  **foreign key** to column `self_id` on table `Self_identifications`. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `artist_id`, `self_id` | PRIMARY |   |
| fk_self_idx | `self_id` | INDEX |   |


## Table: `Self_identifications`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `self_id` | INT | PRIMARY, Not null |   | self-stated identity of the artist, regarding their gender identity and/or sexuality |
| `gender_name` | VARCHAR(30) |  |   | the chosen pronouns used by the artist |
| `gender_description` | VARCHAR(120) |  |   |   |
| `gender_pronoun` | VARCHAR(15) |  |   |   |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `self_id` | PRIMARY |   |


## Table: `Productions`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `prod_id` | INT | PRIMARY, Not null |   | Unique primary key identifier for productions.<br /> |
| `prod_type` | VARCHAR(45) |  |   | Type of production equipment (e.g. software, hardware, instruments, sampling, other equipment). |
| `prod_name` | VARCHAR(45) |  |   | Name of the production equipment (e.g. brand). |
| `prod_model` | VARCHAR(45) |  |   | Model of the production equipment. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `prod_id` | PRIMARY |   |


## Table: `artist_prod`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `artist_id` | INT | PRIMARY, Not null |   | Primary Key for Artist Table, Foreign Key for Artist_Prod<br /><br />**foreign key** to column `artist_id` on table `artists`. |
| `prod_id` | INT | PRIMARY, Not null |   | Primary Key for Productions table, Foreign Key for artist_prod<br /><br />**foreign key** to column `prod_id` on table `Productions`. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `artist_id`, `prod_id` | PRIMARY |   |
| fk_prod_idx | `prod_id` | INDEX |   |


## Table: `artist_genre`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `artist_id` | INT | PRIMARY, Not null |   | primary key – pulls from artists table.<br /><br />**foreign key** to column `artist_id` on table `artists`. |
| `genre_id` | INT | PRIMARY, Not null |   | Primary key – pulls from the genre table.<br /><br />**foreign key** to column `genre_id` on table `genre`. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `artist_id`, `genre_id` | PRIMARY | Associative table linking genre table and artist table. This is similar to many existing 
databases and is important for allowing discovery within a known genre. Many artists change genres over time, so this will also provide interesting historical data.<br /> |
| genre_id_idx | `genre_id` | INDEX |   |


## Table: `affil_id`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `artist_id` | INT | PRIMARY, Not null |   | Pulls from the artists table.<br /><br />**foreign key** to column `artist_id` on table `artists`. |
| `affil_id` | INT | PRIMARY, Not null |   | Pulls from the affiliations table.<br /><br />**foreign key** to column `affil_id` on table `affiliations`. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `artist_id`, `affil_id` | PRIMARY | Associative table linking artists and affiliations. We will need this to see all the places where the artist is engaged over time. For example, some places are gamechangers for new dj's/producers and signal recognition of their skills.<br />There will likely be many affil_id for each artist_id. |
| affil_id_idx | `affil_id` | INDEX |   |


## Table: `social_media`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `social_id` | INT | PRIMARY, Not null |   | Primary Key; social media pages for the artist |
| `social_username` | VARCHAR(45) |  |   | username of the artist on this particular social media site (e.g. Facebook, Twitter, Tumblr, etc.) |
| `social_URL` | VARCHAR(200) |  |   | link to the page of the artist's social media account for this particular site |
| `social_site_name` | VARCHAR(45) |  |   | name of the social media site |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `social_id` | PRIMARY |   |


## Table: `contact_info`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `contact_id` | INT | PRIMARY, Not null |   | Primary Key; describes a method to get in touch with the artist that isn't a social media page |
| `address` | VARCHAR(45) |  |   | Address of this particular contact for this artist |
| `phone_number` | CHAR(10) |  |   | phone number for this particular contact for this artist |
| `contact_name` | VARCHAR(45) |  |   | What kind of contact type is this? (e.g. cell, home, fax) |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `contact_id` | PRIMARY |   |

