

```pa
w = [1, 3, /* ... */]
alpha = 0.01 // learning rate
while notConverged {
		for i in [0 to w.length] {
			g = (d Loss(w)/ d w[i])
			w[i] = w[i] - alpha * g
		}
}
```
