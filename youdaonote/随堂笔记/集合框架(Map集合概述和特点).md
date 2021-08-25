集合框架(Map集合概述和特点)

* A:Map接口概述

	* 查看API可以知道：

		* 将键映射到值的对象

		* 一个映射不能包含重复的键

		* 每个键最多只能映射到一个值

* B:Map接口和Collection接口的不同

	* Map是双列的,Collection是单列的

	* Map的键唯一,Collection的子体系Set是唯一的

	* Map集合的数据结构值针对键有效，跟值无关;Collection集合的数据结构是针对元素有效

	

集合框架(Map集合的功能概述)

* A:Map集合的功能概述

	* a:添加功能

		* V put(K key,V value):添加元素。

			* 如果键是第一次存储，就直接存储元素，返回null

			* 如果键不是第一次存在，就用值把以前的值替换掉，返回以前的值

	* b:删除功能

		* void clear():移除所有的键值对元素

		* V remove(Object key)：根据键删除键值对元素，并把值返回

	* c:判断功能

		* boolean containsKey(Object key)：判断集合是否包含指定的键

		* boolean containsValue(Object value):判断集合是否包含指定的值

		* boolean isEmpty()：判断集合是否为空

	* d:获取功能

		* Set<Map.Entry<K,V>> entrySet():

		* V get(Object key):根据键获取值

		* Set<K> keySet():获取集合中所有键的集合

		* Collection<V> values():获取集合中所有值的集合

	* e:长度功能

		* int size()：返回集合中的键值对的个数





集合框架(Map集合的遍历之键找值)

* A:键找值思路：

	* 获取所有键的集合

	* 遍历键的集合，获取到每一个键

	* 根据键找值

* B:案例演示

	* Map集合的遍历之键找值



			HashMap<String, Integer> hm = new HashMap<>();

			hm.put("张三", 23);

			hm.put("李四", 24);

			hm.put("王五", 25);

			hm.put("赵六", 26);

			

			/*Set<String> keySet = hm.keySet();			//获取集合中所有的键

			Iterator<String> it = keySet.iterator();	//获取迭代器

			while(it.hasNext()) {						//判断单列集合中是否有元素

				String key = it.next();					//获取集合中的每一个元素,其实就是双列集合中的键

				Integer value = hm.get(key);			//根据键获取值

				System.out.println(key + "=" + value);	//打印键值对

			}*/

			

			for(String key : hm.keySet()) {				//增强for循环迭代双列集合第一种方式

				System.out.println(key + "=" + hm.get(key));

			}

	

集合框架(Map集合的遍历之键值对对象找键和值)

* A:键值对对象找键和值思路：

	* 获取所有键值对对象的集合

	* 遍历键值对对象的集合，获取到每一个键值对对象

	* 根据键值对对象找键和值

* B:案例演示

	* Map集合的遍历之键值对对象找键和值

	

			HashMap<String, Integer> hm = new HashMap<>();

			hm.put("张三", 23);

			hm.put("李四", 24);

			hm.put("王五", 25);

			hm.put("赵六", 26);

			/*Set<Map.Entry<String, Integer>> entrySet = hm.entrySet();	//获取所有的键值对象的集合

			Iterator<Entry<String, Integer>> it = entrySet.iterator();//获取迭代器

			while(it.hasNext()) {

				Entry<String, Integer> en = it.next();				//获取键值对对象

				String key = en.getKey();								//根据键值对对象获取键

				Integer value = en.getValue();							//根据键值对对象获取值

				System.out.println(key + "=" + value);

			}*/

			

			for(Entry<String,Integer> en : hm.entrySet()) {

				System.out.println(en.getKey() + "=" + en.getValue());

			}

		

C:源码分析

