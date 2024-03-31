

## Padding tensors for computer vision applications

Create a simple test-tensor that represents two small $2 \times 4$ images:

```
X = torch.tensor(
         [[[1, 1, 1, 1],[1, 1, 1, 1]], [[1, 1, 1, 1],[1, 1, 1, 1]] ]
)
X
```

Output:

```
tensor([[[1, 1, 1, 1],
         [1, 1, 1, 1]],

        [[1, 1, 1, 1],
         [1, 1, 1, 1]]])
```

Now, let's pad two zeros to the top, bottom, left, and right of each image:

```
X = F.pad(torch.tensor(
         [[[1, 1, 1, 1],[1, 1, 1, 1]],
         [[1, 1, 1, 1],[1, 1, 1, 1]] ]), (2,2,2,2), mode='constant', value=0)
X
```

The final output looks as follows:

```
tensor([[[0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 1, 1, 1, 1, 0, 0],
         [0, 0, 1, 1, 1, 1, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0]],

        [[0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 1, 1, 1, 1, 0, 0],
         [0, 0, 1, 1, 1, 1, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0]]])
```
