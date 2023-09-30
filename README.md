# Beam_search_using_python
Beam search only keeps the best n-nodes on the open list, expand all the nodes the ones with the minimum value place them in the open list, if it doesn't have no successor, so remove it from the openlist, expand and go on and on. Beam search algorithm will keep all the successors
# Define the graph as a dictionary of nodes and their neighbors with distances
graph = {
    's': {'a': 3, 'b': 5},
    'a': {'b': 4, 'd': 3},
    'b': {'c': 4},
    'c': {'e': 6},
    'd': {'g': 5},
    'e': {},
    'g': {}
}

# Beam Search algorithm
def beam_search(graph, start, goal, beam_width):
    open_list = [(start, 0, [start])]  # Include the path in the open list
    while open_list:
        open_list.sort(key=lambda x: x[1])  # Sort by path cost
        current_node, current_cost, current_path = open_list.pop(0)

        if current_node == goal:
            return current_path, current_cost

        successors = graph.get(current_node, {})
        successors = [(node, current_cost + cost, current_path + [node]) for node, cost in successors.items()]

        # Keep only the best 'beam_width' successors
        successors.sort(key=lambda x: x[1])
        successors = successors[:beam_width]

        open_list.extend(successors)

    return None

if __name__ == "__main__":
    start_node = 's'
    goal_node = 'g'
    beam_width = 2  # Set the beam width to 2 for Beam Search

    path, total_cost = beam_search(graph, start_node, goal_node, beam_width)

    if path is not None:
        print(f"Found path: {' -> '.join(path)}")
        print(f"Total cost: {total_cost}")
    else:
        print(f"No path found from {start_node} to {goal_node} within the beam width.")


