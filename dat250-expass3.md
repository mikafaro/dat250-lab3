# DAT 250 - Assignment 3 Report

## Step 1

I had a small issue with the versioning of node as I installed it through the ubuntu repositories, and it seems to be a rather old version which didn't work very well with vite. I solved this issue by installing node from a separate repository.

## Step 2

Initially I created the poll application with a few more components than specified in the assignment task. I made reusable components for a button and a card, and I created a tabs component in order to switch between the poll creation form and the poll list. Addidionally, there is a poll details component holding the details of an individual poll that is used inside of the poll list component.

As a first version the svelte app only supports two voting options, and the handling of data is entirely within the front-end. More changes has been needed to integrate it with the back-end. I must either make the decision to expand the front-end to handle user registration and some rudimentary form of login, or handling of user credentials, or I need to bypass this entirely at the back-end and focus only on the polls.

## Step 3

This has been completed by using the @CrossOrigin annotation to the controller classes.

## Step 4

In integrating the frontend and backend I noticed the issue with user management seeing as the previous
assignment required user registration, and the votes and polls to be properties of this class, but this assignment makes
no mention of users at all. In respect of time I decided to alter my backend to bypass the user class when doing http requests
from the front-end. I have successfully set up the poll creation form component to send a post request to the back-end, and for the
poll list to be updated reactively within a few seconds.

When it came to the votes I have not yet been able to retrieve this information correctly from the backend, probably because I've been trying to jsonify a hashmap, which I imagine doesn't just automatically work, so this part requires some more effort later on.

## Step 5

Step 5 not completed yet as I'd like to get the entire app working to a good standard first.
