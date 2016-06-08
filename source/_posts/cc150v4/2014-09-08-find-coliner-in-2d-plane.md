---
layout: post
title: "[CC150v4] 10.6 Find Collinear in 2D Plane"
comments: true
category: CC150v4

---

### Question

> Given a two dimensional graph with points on it, find a line which passes the most number of points. 

### Solution

For this question, we used to use HashMap(Double, Integer) to do. However, the answer suggested in the book define its own Line Class, and uses HashMap(Line, Intger). 

This is a much better solution, however, I failed to write it, don't know why.

__The key is to override the 2 methods__: 

    @override
    public int hashCode() {}
    
    @override
    public boolean equals(Object o) {}

### Code

__not written by me__

Line.java

	public class Line {

		private static double epsilon = .0001;

		public double slope;
		public double intercept;
		private boolean infinite_slope = false;

		public Line(GraphPoint p, GraphPoint q) {
			if (Math.abs(p.x - q.x) > epsilon) { // if x痴 are different
				slope = (p.y - q.y) / (p.x - q.x); // compute slope
				intercept = p.y - slope * p.x; // y intercept from y=mx+b
			} else {
				infinite_slope = true;
				intercept = p.x; // x-intercept, since slope is infinite
			}
		}

		public boolean isEqual(double a, double b) {
			return (Math.abs(a - b) < epsilon);
		}

		public void Print() {
			System.out.println("slope = " + slope + "\nintercept = " + intercept);
		}

		@Override
		public int hashCode() {
			int sl = (int) (slope * 1000);
			int in = (int) (intercept * 1000);
			return sl | in;
		}

		@Override
		public boolean equals(Object o) {
			Line l = (Line) o;
			if (isEqual(l.slope, slope) && isEqual(l.intercept, intercept)
					&& (infinite_slope == l.infinite_slope)) {
				return true;
			}
			return false;
		}
	}

Main method: 

	public static Line findBestLine(GraphPoint[] points) {

		Line bestLine = null;
		HashMap<Line, Integer> line_count = new HashMap<Line, Integer>();

		for (int i = 0; i < points.length; i++) {
			for (int j = i + 1; j < points.length; j++) {
				Line line = new Line(points[i], points[j]);
				if (!line_count.containsKey(line)) {
					line_count.put(line, 0);
				}
				line_count.put(line, line_count.get(line) + 1);
				if (bestLine == null
						|| line_count.get(line) > line_count.get(bestLine)) {
					bestLine = line;
					System.out.println("bestLine upodated! count = "
							+ line_count.get(line));
				}
			}
		}
		return bestLine;
	}
