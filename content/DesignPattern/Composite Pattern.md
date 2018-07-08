---
title: "Composite Pattern"
layout: page
date: 2018-07-08 23:00
---

# 组合模式

网易云音乐的歌单里只能有单曲，不能嵌入其他歌单，太辣鸡了，自己搞一套。

组合模式表现层次结构，能让客户以一致的方式处理个别对象以及对象组合。

(如果是树状结构，可以用栈和递归来实现组合迭代器来遍历整个组合，同时保证层次的层级顺序；考虑用缓存提高遍历效率

# 看代码

定义播放接口，单曲和歌单都应该实现该接口来播放：

```
public interface Playable {
    void play();
}
```

定义单曲和歌单，歌单能添加单曲，并迭代播放所有歌单内的单曲:

```
public class Song implements Playable {

    private String name;

    public Song(String name) {
        this.name = name;
    }

    @Override
    public void play() {
        System.out.println(String.format("播放单曲[%s]", name));
    }
}

public class SongList implements Playable {

    private String name;
    private List<Playable> playList = new ArrayList<Playable>();

    public SongList(String name) {
        this.name = name;
    }

    public void add(Playable song) {
        playList.add(song);
    }

    @Override
    public void play() {
        System.out.println(String.format("播放歌单[%s]", name));
        for (Playable song : playList) {
            song.play();
        }
        System.out.println(String.format("歌单[%s]播放完毕", name));
    }
}

```

测试一下，歌单内也能播放歌单哦:


```
public class Main {
    public static void main(String[] args) {
        SongList songList1 = new SongList("2018");
        songList1.add(new Song("我不希望你孤单的去面对整个喧哗世界"));
        songList1.add(new Song("Luv(sic) Part3"));

        SongList songList2 = new SongList("2018年7月的某个夜晚");
        songList2.add(new Song("I Have The Moon"));

        songList1.add(songList2);

        songList1.play();

    }
}

```

```
播放歌单[2018]
播放单曲[我不希望你孤单的去面对整个喧哗世界]
播放单曲[Luv(sic) Part3]
播放歌单[2018年7月的某个夜晚]
播放单曲[I Have The Moon]
歌单[2018年7月的某个夜晚]播放完毕
歌单[2018]播放完毕
```