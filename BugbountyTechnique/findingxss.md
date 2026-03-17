# Finding XSS

```
gau example.com > urls.txt
```

```
cat urls.txt | wc -l
```

```
echo "example.com" | waybackurls | anew urls.txt
```

```
cat urls.txt | dalfox pipe
```

```
cat urls.txt | gf xss > xss.txt
```

```
cat xss.txt | dalfox pipe
```

- Now whatever URL you get copy and paste and change its query
    ```
    example.com/?s=hello
    ```

    ```
    example.com/?s=<script>alert()</script>
    ```