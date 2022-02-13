# Expected all queries of airbnb in below Picture
![Screenshot (223)](https://user-images.githubusercontent.com/80479635/152977232-85b8a472-1298-4bea-a7ca-6a580f127ea6.png)



# 1. write a query of using two OR operators, and check for listings from any two countries
```js
db.listing.find({ $or: [{'address.country_code': "IN"},{'address.country_code':"US"}]}).count()
```
**o/p - 1222**
```js
db.listing.find({ $or: [{'address.country_code': "IN"},{'address.country_code':"US"},{$or: [{'review_scores.review_scores_rating': {$gte: 90}}]}]}).count()
```
**o/p - 3553**

```js
db.listing.find({ $or: [{'address.country_code': "IN"},{'address.country_code':"US"},{$or: [{'review_scores.review_scores_rating': {$gte: 90}}]}]})
```
**Show the data of following command in below picture**
![Screenshot (213)](https://user-images.githubusercontent.com/80479635/152976583-abd181f6-858b-4dfa-970f-3d27f0fd9b26.png)



# 2. write a query of using two AND operators and check for one country and review ratings to be greater than a particular value
```js
db.listing.find({ $and: [{'address.country_code': "US"},{'review_scores.review_scores_rating': {$gte: 85}}]}).count()
```
**O/P- 1003**

```js
db.listing.find({ $and: [{'address.country_code': "US"},{$and: [{'review_scores.review_scores_rating': {$gte: 60}},{'review_scores.review_scores_rating': {$gte: 90}}]}]}).count()
```
**O/P- 906**

```js
db.listing.find({ $and: [{'address.country_code': "US"},{$and: [{'review_scores.review_scores_rating': {$gte: 60}}]}]}).count()
```
**O/P- 1062**

```js
db.listing.find({ $and: [{'address.country_code': "US"},{$and: [{'review_scores.review_scores_rating': {$gte: 60}}]}]})
```
**Show the data of following command in below picture**
![Screenshot (214)](https://user-images.githubusercontent.com/80479635/152976616-8266642d-ebb4-4e20-81c2-903262676e0b.png)


# 3. write a query of using AND and OR operator in conjuction
    a. it should belong to any two cities and
    b. it should have rating = 99
```js
db.listing.find({ $and: [ {$or: [{'address.country_code': "AU"},{'address.country_code': "US"}]},{'review_scores.review_scores_rating': 99}]}).count()
```
**O/P- 115**

```js
db.listing.find({ $and: [ {$or: [{'address.country_code': "AU"},{'address.country_code': "US"}]},{'review_scores.review_scores_rating': 99}]})
```
**Show the data of following command in below picture**
![Screenshot (215)](https://user-images.githubusercontent.com/80479635/152976677-80426eca-dfff-4ce1-bb30-d212e8de0e08.png)




# 4. write a query of using AND and OR operator together
    a. it should belong to US and rating of 95 or
    b. it should belong to CA and rating of 99

```js
db.listing.find({ $or: [ {$and: [{'address.country_code': "US"},{'review_scores.review_scores_rating': 95}]},{$and: [{'address.country_code': "CA"},{'review_scores.review_scores_rating': 99}]}]}).count()
```
**O/P- 99**

```js
db.listing.find({ $or: [ {$and: [{'address.country_code': "US"},{'review_scores.review_scores_rating': 95}]},{$and: [{'address.country_code': "CA"},{'review_scores.review_scores_rating': 99}]}]},{_id: 1, address: 1, review_scores: 1})
```
**O/P-**
[
  {
    _id: '10166883',
    address: {
      street: 'New York, NY, United States',
      suburb: 'Manhattan',
      government_area: 'East Harlem',
      market: 'New York',
      country: 'United States',
      country_code: 'US',
      location: {
        type: 'Point',
        coordinates: [ -73.93943, 40.79805 ],
        is_location_exact: true
      }
    },
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 9,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 9,
      review_scores_value: 9,
      review_scores_rating: 95
    }
  },
  {
    _id: '10140368',
    address: {
      street: 'Queens, NY, United States',
      suburb: 'Queens',
      government_area: 'Briarwood',
      market: 'New York',
      country: 'United States',
      country_code: 'US',
      location: {
        type: 'Point',
        coordinates: [ -73.82257, 40.71485 ],
        is_location_exact: true
      }
    },
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 9,
      review_scores_value: 10,
      review_scores_rating: 95
    }
  },
**Show the data of following command in below picture**
![Screenshot (216)](https://user-images.githubusercontent.com/80479635/152976717-dd838f22-7ea5-4036-a20b-418fcfb8b858.png)
![Screenshot (217)](https://user-images.githubusercontent.com/80479635/152976736-fc0c6927-028b-490c-8d50-0ea777470c34.png)



# 5. write a query of using querying arrays
    a. check all listings which have amenities of size 5, 6, 7, 8, 9, 10
    b. check all listings of where aminities contain 4 or 5 different listings 
    c. check all listings of reviews where it matches a particular user id and name 
    d. check all listings of reviews where it matches a particular user id and name, list only reviews that match the particular user id and name

- # a.
```js
db.listing.find({$or: [{'amenities':{$size: 5}},{'amenities': {$size: 6}},{'amenities': {$size: 7}},{'amenities': {$size: 8}},{'amenities': {$size: 9}},{'amenities': {$size: 10}}]},{amenities: 1}).count()        
```
**O/P- 657**

```js
db.listing.find({'amenities':{$size: 5}},{amenities: 1}).count()
```
**O/P- 31**

```js
db.listing.find({'amenities':{$size: 6}},{amenities: 1}).count()
```
**O/P- 50**

```js
db.listing.find({'amenities':{$size: 7}},{amenities: 1}).count()
```
**O/P- 86**

```js
db.listing.find({'amenities':{$size: 8}},{amenities: 1}).count()
```
**O/P- 117**

```js
db.listing.find({'amenities':{$size: 9}},{amenities: 1}).count()
```
**O/P- 168**

```js
db.listing.find({'amenities':{$size: 10}},{amenities: 1}).count()
```
**O/P- 205**


# b.
```js
db.listing.find({$or: [{'amenities':{$size: 4}},{'amenities': {$size: 5}}]},{amenities: 1}).count()   
```
**O/P- 47**


# c.
```js
db.listing.find({'reviews':{$elemMatch: { _id: '420508856',reviewer_name: "Joe"}}},{_id: 0, reviews: 1}).count()
```
**O/P- 1**

```js
db.listing.find({'reviews':{$elemMatch: { _id: '420508856',reviewer_name: "Joe"}}},{_id: 0, 'reviews.reviewer_name': 1})
```
**Show the data of following command in below picture**
![Screenshot (218)](https://user-images.githubusercontent.com/80479635/152976808-271ed672-18eb-481e-ba80-6a5b06dd98dc.png)
![Screenshot (219)](https://user-images.githubusercontent.com/80479635/152976842-0a081fdd-4792-4c5b-aae6-38861a952237.png)
![Screenshot (220)](https://user-images.githubusercontent.com/80479635/152976854-0d579e64-c405-4475-887a-cb7828832289.png)



# d.
```js
db.listing.find({'reviews':{$elemMatch: { _id: '420508856',reviewer_name: "Joe"}}},{reviews: {$elemMatch: {_id: '420508856',reviewer_name: "Joe"}}})
```
**O/P-**

[
  {
    _id: '10108388',
    reviews: [
      {
        _id: '420508856',
        date: ISODate("2019-03-06T05:00:00.000Z"),
        listing_id: '10108388',
        reviewer_id: '35883709',
        reviewer_name: 'Joe',
        comments: "I highly recommend Desiree's place to anyone visiting Sydney.  It's convenient, clean, and very comfortable.  Desiree was an outstanding host.  She was communicative, helpful, and went above and beyond.  I hope to return."
      }
    ]
  }
]



# 6. find top 10 listings, sort them according to rating in descending order, and if the rating is similar rate them according to alphabetic order
    a. also ensure results belong only to New York, and check if there are atleast Wifi, Breakfast and 2 other amenities

```js
db.listing.find({},{_id:1,review_scores: 1,name: 1}).sort({'review_scores.review_scores_rating': -1}).limit(10)
```
**Show same rating**

```js
db.listing.find({},{_id:1,review_scores: 1,name: 1}).sort({'review_scores.review_scores_rating': -1,name: 1}).limit(10)
```
**O/P-**

[
  {
    _id: '32297024',
    name: '!Luxury Studio @Central  steps from Escalator',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 9,
      review_scores_value: 9,
      review_scores_rating: 100
    }
  },
  {
    _id: '2123266',
    name: '"GREAT LOCATION COPACABANA BEACH = 60m2 =4 people"',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 9,
      review_scores_rating: 100
    }
  },
  {
    _id: '18316061',
    name: '"Gorgeous and artfully styled oasis ...."',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 9,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '21675318',
    name: '( ͡° ͜ʖ ͡°) Baaasic Spaaace (ฅ´ω`ฅ)',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '29508303',
    name: '*COSY ROOM with Private Toilet and Balcony',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '23921295',
    name: '-MAISON ALEXANDRA- 3 STOREY WATERFRONT PH FLOOR',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '3530395',
    name: '1 BR in Great NYC Neighborhood',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '32546486',
    name: '1 Bdr Cozy condo,Five-Star Home,convenient,in DT!!',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '27864530',
    name: '1 Bed Studio in Perfect Location!',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '4217268',
    name: '1 Bedroom Apartment in Washington Heights - Summer',
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  }
]

# a.
```js
db.listing.find({'address.market': {$eq: "New York"},'amenities':{$all:['Wifi', 'Shampoo','Internet','Kitchen' ]}},{_id:1,review_scores: 1,name: 1,amenities: 1}).sort({'review_scores.review_scores_rating': -1,name: 1}).limit(10) 
```
**O/P->**
[
  {
    _id: '3530395',
    name: '1 BR in Great NYC Neighborhood',
    amenities: [
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Buzzer/wireless intercom',
      'Heating',
      'Smoke detector',
      'First aid kit',
      'Safety card',
      'Essentials',
      'Shampoo'
    ],
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '20275670',
    name: 'Amazing Studio step away from Time Square/53C',
    amenities: [
      'TV',
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Elevator',
      'Heating',
      'Smoke detector',
      'Carbon monoxide detector',
      'Fire extinguisher',
      'Essentials',
      'Shampoo',
      'Hangers',
      'Hair dryer',
      'Iron',
      'Laptop friendly workspace',
      'Hot water',
      'Bed linens',
      'Extra pillows and blankets',
      'Microwave',
      'Coffee maker',
      'Refrigerator',
      'Dishes and silverware',
      'Cooking basics',
      'Oven',
      'Stove',
      'Luggage dropoff allowed',
      'Long term stays allowed',
      'Host greets you'
    ],
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '6610629',
    name: 'Art Gallery  in Harlem',
    amenities: [
      'TV',
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Buzzer/wireless intercom',
      'Heating',
      'Smoke detector',
      'Carbon monoxide detector',
      'First aid kit',
      'Fire extinguisher',
      'Essentials',
      'Shampoo'
    ],
    review_scores: {
      review_scores_accuracy: 8,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 9,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '2453739',
    name: 'Awesome Child Friendly Apartment!',
    amenities: [
      'TV',
      'Internet',
      'Wifi',
      'Air conditioning',
      'Wheelchair accessible',
      'Kitchen',
      'Elevator',
      'Free street parking',
      'Buzzer/wireless intercom',
      'Heating',
      'Family/kid friendly',
      'Washer',
      'Dryer',
      'Smoke detector',
      'Carbon monoxide detector',
      'First aid kit',
      'Essentials',
      'Shampoo',
      'Hangers',
      'Hair dryer',
      'Iron',
      'Laptop friendly workspace',
      'Private entrance',
      'Bathtub',
      'Children’s books and toys',
      'Babysitter recommendations',
      'Room-darkening shades',
      'Hot water',
      'Bed linens',
      'Extra pillows and blankets',
      'Coffee maker',
      'Refrigerator',
      'Dishes and silverware',
      'Cooking basics',
      'Oven',
      'Stove',
      'Wide hallway clearance',
      'Step-free access',
      'Wide doorway',
      'Flat path to front door',
      'Well-lit path to entrance',
      'Step-free access',
      'Step-free access',
      'Wide entryway',
      'Host greets you'
    ],
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 9,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '289703',
    name: 'Beautiful SoHo Luxury Apartment',
    amenities: [
      'TV',
      'Cable TV',
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Doorman',
      'Pets live on this property',
      'Dog(s)',
      'Elevator',
      'Buzzer/wireless intercom',
      'Heating',
      'Family/kid friendly',
      'Washer',
      'Dryer',
      'Smoke detector',
      'Essentials',
      'Shampoo',
      '24-hour check-in',
      'Hangers',
      'Hair dryer',
      'Iron',
      'Laptop friendly workspace'
    ],
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '7867805',
    name: 'Best location in manhattan',
    amenities: [
      'TV',
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Heating',
      'First aid kit',
      'Fire extinguisher',
      'Essentials',
      'Shampoo',
      '24-hour check-in',
      'Hair dryer',
      'Iron',
      'Laptop friendly workspace'
    ],
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '19877706',
    name: 'Big 3 Bedroom Garden Level Apartment Near Subway',
    amenities: [
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Free parking on premises',
      'Indoor fireplace',
      'Heating',
      'Family/kid friendly',
      'Smoke detector',
      'Carbon monoxide detector',
      'Fire extinguisher',
      'Essentials',
      'Shampoo',
      'Lock on bedroom door',
      'Hangers',
      'Hair dryer',
      'Iron',
      'Laptop friendly workspace',
      'Self check-in',
      'Keypad',
      'Private entrance',
      'Hot water',
      'Bed linens',
      'Extra pillows and blankets',
      'Long term stays allowed'
    ],
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '14894267',
    name: 'Doorman, modern apart. on Broadway (Central Park)',
    amenities: [
      'TV',
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Doorman',
      'Gym',
      'Elevator',
      'Heating',
      'Washer',
      'Dryer',
      'Smoke detector',
      'Carbon monoxide detector',
      'Fire extinguisher',
      'Essentials',
      'Shampoo',
      '24-hour check-in',
      'Hangers',
      'Iron',
      'Laptop friendly workspace',
      'translation missing: en.hosting_amenity_49',
      'translation missing: en.hosting_amenity_50',
      'Self check-in',
      'Building staff',
      'Microwave',
      'Coffee maker',
      'Refrigerator',
      'Dishwasher',
      'Dishes and silverware',
      'Cooking basics',
      'Oven',
      'Stove',
      'Step-free access',
      'Wide doorway',
      'Flat path to front door',
      'Step-free access',
      'Wide doorway',
      'Accessible-height toilet',
      'Wide clearance to shower',
      'toilet',
      'Step-free access',
      'Wide entryway',
      'Handheld shower head',
      'Paid parking on premises'
    ],
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 9,
      review_scores_rating: 100
    }
  },
  {
    _id: '11005300',
    name: 'East Village Sanctuary',
    amenities: [
      'TV',
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Heating',
      'Smoke detector',
      'Carbon monoxide detector',
      'Essentials',
      'Shampoo',
      '24-hour check-in',
      'Hangers',
      'Hair dryer',
      'Iron',
      'Laptop friendly workspace',
      'Hot water',
      'Long term stays allowed',
      'Other'
    ],
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  },
  {
    _id: '6376606',
    name: 'Gramercy Apt, Private Bedroom',
    amenities: [
      'TV',
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Buzzer/wireless intercom',
      'Heating',
      'Smoke detector',
      'Essentials',
      'Shampoo'
    ],
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 10,
      review_scores_value: 10,
      review_scores_rating: 100
    }
  }
]

**Below Picture shows above query details**
![Screenshot (221)](https://user-images.githubusercontent.com/80479635/152977011-d5883685-4f25-4ca5-a906-2f06b7ddbcc8.png)
![Screenshot (222)](https://user-images.githubusercontent.com/80479635/152977024-889e3930-9bb0-4446-b9ef-4eea4eef5249.png)
