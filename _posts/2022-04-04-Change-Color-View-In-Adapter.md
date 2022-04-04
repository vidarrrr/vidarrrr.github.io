---
layout: post
title: Change Color in getView of Adapter
---

Let's say you getView function like these:
```
public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
     View view = convertView;
        if(view==null){
            view = LayoutInflater.from(mContext).inflate(resourceLayout,parent,false);
        }
        
        String textViewText = getItem(position);
        if(textViewText.contains("abc"){
            view.setBackgroundColor(Color.BLACK);
        }
        
        ...
}
```
with this code we will have problem with views 
<pre>
abd -> white                                           abe -> white 
abe -> white                                           abd -> white
abc -> black                                           abd -> black    ???????
abd -> white   showed 6 items and scrolled by user =>  abd -> white
abd -> white                                           abd -> white
abd -> white                                           abd -> white
</pre>
because we didn't implement else partion and not changed old view :

```
public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        View view = convertView;
        if(view==null){
            view = LayoutInflater.from(mContext).inflate(resourceLayout,parent,false);
        }
        
        String textViewText = getItem(position);
        if(textViewText.contains("abc"){
            view.setBackgroundColor(Color.BLACK);
        }else{
            view.setBackgroundColor(Color.TRANSPARENT);
        }
        
        ...
}

```




