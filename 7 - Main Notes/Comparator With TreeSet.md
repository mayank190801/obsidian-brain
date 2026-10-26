
2024-06-26 08:24
Status: #baby 
Tags: [[data structures]]

# Comparator With TreeSet

```
TreeSet<Pair> set = new TreeSet<>(new Comparator<Pair>() {
    @Override
    public int compare(Pair o1, Pair o2) {
        return o1.b - o2.b; 
    }
});
```

# **References**