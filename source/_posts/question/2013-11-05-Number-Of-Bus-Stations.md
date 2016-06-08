---
layout: post
title: "[Question] Number Of Bus Stations (meeting rooms) "
comments: true
category: Question

---

### Question 

[link](http://tech-queries.blogspot.sg/2009/05/number-of-bus-stations.html)

> At a bus-station, you have time-table for buses arrival and departure. You need to find the minimum number of platforms so that all the buses can be accommodated as per their schedule. 

> Example: Time table is like below:

    Bus         Arrival         Departure 
    BusA        0900 hrs        0930 hrs
    BusB        0915 hrs        1300 hrs
    BusC        1030 hrs        1100 hrs
    BusD        1045 hrs        1145 hrs

> The answer must be 3. 

This question can also be in other forms: 

> Given a vector of Nodes, each of which contain the start and end time of a meeting, find the maximum number of rooms one would have to book for the day. 

### Solution

The answer is same as finding the maximum number of bus at the bus-station at the same time. 

__The suggestted solution__ from [here](http://tech-queries.blogspot.sg/2009/05/number-of-bus-stations.html): 

> So first sort all the arrival(A) and departure(D) time in an int array. Please save the corresponding arrival or departure in the array also. 

> After sorting our array will look like this:

    0900    0915    1930    1030    1045    1100    1145    1300
    A       A       D       A       A       D       D       D

Now use a counter. When sees an A, increment. When sees an D, decreament. In the end, return the largest counter value. 

Note: If you have a arriving and a departing at same time, put departure time first.

### code

	public int solve(List<Meeting> input) {
		List<Event> events = new ArrayList<Event>();
		for (Meeting i : input) {
			events.add(new Event(i.start, 1));
			events.add(new Event(i.end, -1));
		}
		Collections.sort(events);

		int currentNeeds = 0;
		int maxNeeds = 0;
		for (Event e : events) {
			currentNeeds += e.diff;
			maxNeeds = Math.max(maxNeeds, currentNeeds);
		}
		return maxNeeds;
	}

supporting classes:

    class Event implements Comparable<Event> {
        int time;
        int diff;
        // variable diff have value of 1 or -1
        // when = 1, it means starting a meeting and 1 more room needed
        // when = -1, it means ending a meeting and 1 less room needed

        public Event(int a, int b) {
            time = a;
            diff = b;
        }

        @Override
        public int compareTo(Event o) {
            if (this.time == o.time) {
                return this.diff - o.diff;
            }
            return this.time - o.time;
        }
    }

    class Meeting {
        int start;
        int end;

        public Meeting(int a, int b) {
            start = a;
            end = b;
        }
    }
