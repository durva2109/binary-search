# binary-search

# CHICKEN DIVISION CODE

import random
            
def chicken_weight_sort(chicken_weights):
    if len(chicken_weights) <= 1:
        return chicken_weights
            
    mid = len(chicken_weights) // 2
    left_half = chicken_weights[:mid]
    right_half = chicken_weights[mid:]
            
    left_half = chicken_weight_sort(left_half)
    right_half = chicken_weight_sort(right_half)
            
    return merge(left_half, right_half)
            
def merge(left, right):
    merged = []
    left_index = right_index = 0
            
    while left_index < len(left) and right_index < len(right):
        if left[left_index] < right[right_index]:
            merged.append(left[left_index])
            left_index += 1
        else:
            merged.append(right[right_index])
            right_index += 1

    merged.extend(left[left_index:])
    merged.extend(right[right_index:])

    return merged

def binary_search(chicken_weights, target):
    low = 0
    high = len(chicken_weights) - 1

    while low <= high:
        mid = (low + high) // 2
        if abs(chicken_weights[mid] - target) < 0.01:  # for int - chicken_weights[mid] == target:
            return mid
        elif chicken_weights[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
            
    return -1

if __name__ == '__main__':
    # Generate random chicken weights ranging from 1.0 to 5.0 with odecimal places
    chicken_weights = [round(random.uniform(1.0, 5.0), 1) for _ in range(15)]
    sorted_chicken_weights = chicken_weight_sort(chicken_weights)
    print("\n .............................................\n", "!!! WELCOME TO JAMAL HALAL CHICKEN CENTRE !!!\n", ".............................................")
    target_weight = float(input("\n Enter the weight of the chicken you want (or enter -1 to exit): "))  # Parse input as float
    if target_weight != -1:
        index = binary_search(sorted_chicken_weights, target_weight)
        if index != -1:
            print(f"\nFound chicken with weight {target_weight:.2f} at index {index}.")
        else:
            print(f"\n Sorry !!!\n Chicken with weight {target_weight:.2f} not found in our chicken's rack. :(\n","Here's the list of chicken weights that we have : \n", sorted_chicken_weights)
            print("\n Thank you for visiting Jamal Halal Chicken Centre. Have a great day! :)")
    else:
        print("\n Thank you for visiting Jamal Halal Chicken Centre. Have a great day! :)")
            
        
