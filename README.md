#ExpNo:10 Implementation of Classical Planning Algorithm 

NAME:  KANISHKA P

REG NO: 2305001011

## AIM:
To implement classical planning algorithm for practical real-life situations

## Classical Planning Algorithm:
Classical Planning is a fundamental concept in Artificial Intelligence (AI) that focuses on finding an optimal sequence of actions to reach a desired goal from an initial state. It assumes a deterministic, fully observable and static environment where the agent knows exactly how each action affects the world.

It contains:

State: Represents the configuration of the world at a specific time i.e all facts that are currently true.

Action: Defines transitions between states. Each action has Preconditions (what must be true before it executes.) and Effect (show the action changes the world.).

Goal: The desired end-state that satisfies the planner’s objective.

Plan: A sequence of actions that transitions the system from the initial state to the goal while satisfying all constraints.

## Algorithm or Steps Involved:
Step-1: Define the initial state

Step-2: Define the goal state

Step-3: Define the actions

Step-4: Find a plan to reach the goal state

Step-5: Print the plan

### Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
Output:
['move_A_to_B']
```

### Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
Output:
['move_A_to_B', 'move_B_to_C']
```

### PROGRAM
```

def is_goal_state(current_state, goal_state):
    return all(current_state.get(k) == v for k, v in goal_state.items())


def apply_action(current_state, effect):
    new_state = current_state.copy()
    new_state.update(effect)
    return new_state


def is_applicable(current_state, precondition):
    return all(current_state.get(k) == v for k, v in precondition.items())


def find_plan(initial_state, goal_state, actions):
    queue = [(initial_state, [])]
    visited = set()

    while queue:
        current_state, plan = queue.pop(0)

        # Check goal
        if is_goal_state(current_state, goal_state):
            return plan

        # Mark visited
        state_tuple = tuple(sorted(current_state.items()))
        if state_tuple in visited:
            continue
        visited.add(state_tuple)

        # Expand actions
        for action_name, action_data in actions.items():
            if is_applicable(current_state, action_data['precondition']):
                next_state = apply_action(current_state, action_data['effect'])
                queue.append((next_state, plan + [action_name]))

    return None


# ---------------------------------------------------------
# TEST CASE 1
# ---------------------------------------------------------

initial_state = {'A': 'Table', 'B': 'Table'}

goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {
        'precondition': {'A': 'Table', 'B': 'Table'},
        'effect': {'A': 'B'}
    }
}

print("PLAN 1:", find_plan(initial_state, goal_state, actions))


# ---------------------------------------------------------
# TEST CASE 2
# ---------------------------------------------------------

initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}

goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {
        'precondition': {'A': 'Table', 'B': 'Table'},
        'effect': {'A': 'B'}
    },
    'move_B_to_C': {
        'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'},
        'effect': {'B': 'C'}
    }
}

print("PLAN 2:", find_plan(initial_state, goal_state, actions))
```

### OUTPUT

<img width="789" height="69" alt="image" src="https://github.com/user-attachments/assets/a2d7c494-2d9f-4156-93fb-45825d508bf3" />


### RESULT
Thus the program to implement Classical Planning Algorithm has been executed successfully.

