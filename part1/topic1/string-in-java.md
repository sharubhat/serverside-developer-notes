# String in java - java.lang.String

### substring\(\) in java

In jdk1.6, when substring\(int beginIndex\) or substring\(int beginIndex, int endIndex\) is called, it creates a new String object which refers to same old character array on heap. If we only need a very small portion of long String, we end up keeping the original very long string in memory. However, this is improved in jdk1.7 and jdk1.8 where it actually creates a new String which points to a new character array.

