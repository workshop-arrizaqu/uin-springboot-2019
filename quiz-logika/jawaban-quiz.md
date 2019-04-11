# Jawaban Quiz

```java
public int[] getMaxValues(int[] dataFib) {
    int[] data = new int[2];
    int hasil = 0;
    for(int i = 0; i < dataFib.length; i++) {
        hasil = hasil + dataFib[i]; 
    }

    data[0] = dataFib.length;
    data[1] = hasil;

    return data;
}
```

## Contoh Hasil : 

![](/assets/jawaban)



