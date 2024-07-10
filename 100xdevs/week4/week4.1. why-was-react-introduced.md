---
title: react and state management
tags:
  - react
  - frontend
  - state-management
---
<img src="./the discovery of gravity, painting, two color.jpg" width="400px" height="400px"/>


- Why React  was introduced ? 
	- DOM operations are expensive.
	- very hard for application developer to modify DOM and the reconciler to mutate the state variables and make changes dynamically.
- Updating the DOM is very hard 
	- Need a reconciler for the update operations to maintain the global state
	- removing ,adding to the DOM directly is very expensive and 
	- the idea is to only apply the diff of the changes, not re-create everything
- 