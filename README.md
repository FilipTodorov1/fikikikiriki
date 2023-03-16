# fikikikirikidef transform_array(A, B):
    n = len(A)
    min_steps = float('inf')

    # Shift A to the right and update min_steps
    for i in range(n):
        A = [A[-1]] + A[:-1]
        steps = i + abs(B[0]-A[0])
        if steps >= min_steps:
            break
        if A == B:
            min_steps = steps

    # Reset A to its original state
    A = A[-1:] + A[:-1]

    # Increment or decrement elements of A and update min_steps
    for i in range(n):
        steps = abs(B[i]-A[i])
        if steps >= min_steps:
            break
        if (B[i]-A[i]) % n != steps % n:
            steps += n
        min_steps = min(min_steps, steps)

        if B[i] > A[i]:
            A[i] += steps
        else:
            A[i] -= steps

    return min_steps
