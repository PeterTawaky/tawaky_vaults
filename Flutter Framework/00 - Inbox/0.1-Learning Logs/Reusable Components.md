---
tags:
  - flutter-concepts
parent: 
type: Permanent Note
deeper: 
against:
---
### Why Reusable Components:
1. reduce time 
2. clean code
3. the components of the app is the same in the whole app
4. easy to make changes in this app
### Two Methods to apply this:
	1. create a function that takes parameters and return the `Reusable Widget`
	2. put it in special class and take data by constractor ✅✅(Model)
### what to take care of:
- what is the optional fields and what is the required fields
- what is the changed properties among the component widget that will become your fields
- use initial default value to the fields or not
- this component changes in UI or not
	- stateless (doesn't change)
	- `stateful` (change)