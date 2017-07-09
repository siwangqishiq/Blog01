
## 基于有限状态机的字符串搜索算法
&nbsp&nbsp &nbsp&nbsp 字符串匹配问题 , 在一个指定的字符串P中寻找是否存在子串T，若存在,返回T在P中第一次出现的位置，若不存,返回-1, 典型应用便是在一段文章中查找关键字.
	    
	  int indexOf(char *t,int len,char *p,int pLen) {
		if(!pLen)
			return -1;
			int max = len - pLen;
		
		if(max < 0)
			return -1;
	
		for(int i = 0;i <= max; i++){
			int j = 0;
			int index = 0;
			while(index < pLen && t[i + index] == p[index]){
				index++;
			}//end while
			if(index == pLen)
				return i;
		}//end for i
	
		return -1;
	  }	    
以上是c实现的一个典型的字符串匹配算法 ，目前 `java sdk` 中的 `String` 类提供的 `indexOf`方法也是采用了类似的实现，从主串T出发，若找到的字符与P第一个字符相同，进入下一层循环，判断此后的字符是否也都相同，若相同则返回找到的位置坐标，若不同则退出内层循环，继续处理P的后一个字符。
<p>此算法时间复杂度为![](http://latex.codecogs.com/gif.latex?\Theta(mn)) 其中 m代表P串的长度，n代表T串长度。本身可以满足大部分场景，但是当搜索串T,和模式串P长度值极大时，算法效率就会下降很多，下面介绍的有限状态自动机算法可以在自动机已经建立的前提下，实现![](http://latex.codecogs.com/gif.latex?\Theta(n))的算法。
<p>
先来看看有限状态自动机的定义

   


