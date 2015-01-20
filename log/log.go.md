# function itoa
此方法是将int(integer)原始类型转化成ascii。

其实该方法是通过rune转化的，只不过范围在'0'~'9'的rune所占的字节数都为1，因此用一个byte储存即可。

```go
// i的长度超过wid的时，wid不起作用。而是全部显示。
// i的长度不超过wid的时，前面的byte用'0'填充
func itoa(buf *[]byte, i int, wid int) {
	var u uint = uint(i)
	if u == 0 && wid <= 1 {
		*buf = append(*buf, '0')
		return
	}

	// Assemble decimal in reverse order.
	var b [32]byte
	bp := len(b)
	for ; u > 0 || wid > 0; u /= 10 {
		bp--
		wid--
		b[bp] = byte(u%10) + '0'
	}
	*buf = append(*buf, b[bp:]...)
}
```