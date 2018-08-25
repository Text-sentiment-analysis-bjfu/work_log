## Array 简介

PHP Array 函数允许您访问并操作数组。

支持简单的数组和多维数组。

### 安装

------

PHP Array 函数是 PHP 核心的组成部分。无需安装即可使用这些函数。

------

### PHP 5 Array 函数

------
| 函数                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [array()](http://www.runoob.com/php/func-array.html)         | 创建数组。                                                   |
| [array_change_key_case()](http://www.runoob.com/php/func-array-change-key-case.html) | 返回其键均为大写或小写的数组。                               |
| [array_chunk()](http://www.runoob.com/php/func-array-chunk.html) | 把一个数组分割为新的数组块。                                 |
| [array_column()](http://www.runoob.com/php/func-array-column.html) | 返回输入数组中某个单一列的值。                               |
| [array_combine()](http://www.runoob.com/php/func-array-combine.html) | 通过合并两个数组（一个为键名数组，一个为键值数组）来创建一个新数组。 |
| [array_count_values()](http://www.runoob.com/php/func-array-count-values.html) | 用于统计数组中所有值出现的次数。                             |
| [array_diff()](http://www.runoob.com/php/func-array-diff.html) | 比较数组，返回两个数组的差集（只比较键值）。                 |
| [array_diff_assoc()](http://www.runoob.com/php/func-array-diff-assoc.html) | 比较数组，返回两个数组的差集（比较键名和键值）。             |
| [array_diff_key()](http://www.runoob.com/php/func-array-diff-key.html) | 比较数组，返回两个数组的差集（只比较键名）。                 |
| [array_diff_uassoc()](http://www.runoob.com/php/func-array-diff-uassoc.html) | 比较数组，返回两个数组的差集（比较键名和键值，使用用户自定义的键名比较函数）。 |
| [array_diff_ukey()](http://www.runoob.com/php/func-array-diff-ukey.html) | 比较数组，返回两个数组的差集（只比较键名，使用用户自定义的键名比较函数）。 |
| [array_fill()](http://www.runoob.com/php/func-array-fill.html) | 用给定的键值填充数组。                                       |
| [array_fill_keys()](http://www.runoob.com/php/func-array-fill-keys.html) | 用给定的指定键名的键值填充数组。                             |
| [array_filter()](http://www.runoob.com/php/func-array-filter.html) | 用回调函数过滤数组中的元素。                                 |
| [array_flip()](http://www.runoob.com/php/func-array-flip.html) | 反转/交换数组中的键名和对应关联的键值。                      |
| [array_intersect()](http://www.runoob.com/php/func-array-intersect.html) | 比较数组，返回两个数组的交集（只比较键值）。                 |
| [array_intersect_assoc()](http://www.runoob.com/php/func-array-intersect-assoc.html) | 比较数组，返回两个数组的交集（比较键名和键值）。             |
| [array_intersect_key()](http://www.runoob.com/php/func-array-intersect-key.html) | 比较数组，返回两个数组的交集（只比较键名）。                 |
| [array_intersect_uassoc()](http://www.runoob.com/php/func-array-intersect-uassoc.html) | 比较数组，返回两个数组的交集（比较键名和键值，使用用户自定义的键名比较函数）。 |
| [array_intersect_ukey()](http://www.runoob.com/php/func-array-intersect-ukey.html) | 比较数组，返回两个数组的交集（只比较键名，使用用户自定义的键名比较函数）。 |
| [array_key_exists()](http://www.runoob.com/php/func-array-key-exists.html) | 检查指定的键名是否存在于数组中。                             |
| [array_keys()](http://www.runoob.com/php/func-array-keys.html) | 返回数组中所有的键名。                                       |
| [array_map()](http://www.runoob.com/php/func-array-map.html) | 将用户自定义函数作用到给定数组的每个值上，返回新的值。       |
| [array_merge()](http://www.runoob.com/php/func-array-merge.html) | 把一个或多个数组合并为一个数组。                             |
| [array_merge_recursive()](http://www.runoob.com/php/func-array-merge-recursive.html) | 递归地把一个或多个数组合并为一个数组。                       |
| [array_multisort()](http://www.runoob.com/php/func-array-multisort.html) | 对多个数组或多维数组进行排序。                               |
| [array_pad()](http://www.runoob.com/php/func-array-pad.html) | 将指定数量的带有指定值的元素插入到数组中。                   |
| [array_pop()](http://www.runoob.com/php/func-array-pop.html) | 删除数组中的最后一个元素（出栈）。                           |
| [array_product()](http://www.runoob.com/php/func-array-product.html) | 计算数组中所有值的乘积。                                     |
| [array_push()](http://www.runoob.com/php/func-array-push.html) | 将一个或多个元素插入数组的末尾（入栈）。                     |
| [array_rand()](http://www.runoob.com/php/func-array-rand.html) | 从数组中随机选出一个或多个元素，返回键名。                   |
| [array_reduce()](http://www.runoob.com/php/func-array-reduce.html) | 通过使用用户自定义函数，迭代地将数组简化为一个字符串，并返回。 |
| [array_replace()](http://www.runoob.com/php/func-array-replace.html) | 使用后面数组的值替换第一个数组的值。                         |
| [array_replace_recursive()](http://www.runoob.com/php/func-array-replace-recursive.html) | 递归地使用后面数组的值替换第一个数组的值。                   |
| [array_reverse()](http://www.runoob.com/php/func-array-reverse.html) | 将原数组中的元素顺序翻转，创建新的数组并返回。               |
| [array_search()](http://www.runoob.com/php/func-array-search.html) | 在数组中搜索给定的值，如果成功则返回相应的键名。             |
| [array_shift()](http://www.runoob.com/php/func-array-shift.html) | 删除数组中的第一个元素，并返回被删除元素的值。               |
| [array_slice()](http://www.runoob.com/php/func-array-slice.html) | 返回数组中的选定部分。                                       |
| [array_splice()](http://www.runoob.com/php/func-array-splice.html) | 把数组中的指定元素去掉并用其它值取代。                       |
| [array_sum()](http://www.runoob.com/php/func-array-sum.html) | 返回数组中所有值的和。                                       |
| [array_udiff()](http://www.runoob.com/php/func-array-udiff.html) | 比较数组，返回两个数组的差集（只比较键值，使用一个用户自定义的键名比较函数）。 |
| [array_udiff_assoc()](http://www.runoob.com/php/func-array-udiff-assoc.html) | 比较数组，返回两个数组的差集（比较键名和键值，使用内建函数比较键名，使用用户自定义函数比较键值）。 |
| [array_udiff_uassoc()](http://www.runoob.com/php/func-array-udiff-uassoc.html) | 比较数组，返回两个数组的差集（比较键名和键值，使用两个用户自定义的键名比较函数）。 |
| [array_uintersect()](http://www.runoob.com/php/func-array-uintersect.html) | 比较数组，返回两个数组的交集（只比较键值，使用一个用户自定义的键名比较函数）。 |
| [array_uintersect_assoc()](http://www.runoob.com/php/func-array-uintersect-assoc.html) | 比较数组，返回两个数组的交集（比较键名和键值，使用内建函数比较键名，使用用户自定义函数比较键值）。 |
| [array_uintersect_uassoc()](http://www.runoob.com/php/func-array-uintersect-uassoc.html) | 比较数组，返回两个数组的交集（比较键名和键值，使用两个用户自定义的键名比较函数）。 |
| [array_unique()](http://www.runoob.com/php/func-array-unique.html) | 删除数组中重复的值。                                         |
| [array_unshift()](http://www.runoob.com/php/func-array-unshift.html) | 在数组开头插入一个或多个元素。                               |
| [array_values()](http://www.runoob.com/php/func-array-values.html) | 返回数组中所有的值。                                         |
| [array_walk()](http://www.runoob.com/php/func-array-walk.html) | 对数组中的每个成员应用用户函数。                             |
| [array_walk_recursive()](http://www.runoob.com/php/func-array-walk-recursive.html) | 对数组中的每个成员递归地应用用户函数。                       |
| [arsort()](http://www.runoob.com/php/func-array-arsort.html) | 对关联数组按照键值进行降序排序。                             |
| [asort()](http://www.runoob.com/php/func-array-asort.html)   | 对关联数组按照键值进行升序排序。                             |
| [compact()](http://www.runoob.com/php/func-array-compact.html) | 创建一个包含变量名和它们的值的数组。                         |
| [count()](http://www.runoob.com/php/func-array-count.html)   | 返回数组中元素的数目。                                       |
| [current()](http://www.runoob.com/php/func-array-current.html) | 返回数组中的当前元素。                                       |
| [each()](http://www.runoob.com/php/func-array-each.html)     | 返回数组中当前的键／值对。                                   |
| [end()](http://www.runoob.com/php/func-array-end.html)       | 将数组的内部指针指向最后一个元素。                           |
| [extract()](http://www.runoob.com/php/func-array-extract.html) | 从数组中将变量导入到当前的符号表。                           |
| [in_array()](http://www.runoob.com/php/func-array-in-array.html) | 检查数组中是否存在指定的值。                                 |
| [key()](http://www.runoob.com/php/func-array-key.html)       | 从关联数组中取得键名。                                       |
| [krsort()](http://www.runoob.com/php/func-array-krsort.html) | 对关联数组按照键名降序排序。                                 |
| [ksort()](http://www.runoob.com/php/func-array-ksort.html)   | 对关联数组按照键名升序排序。                                 |
| [list()](http://www.runoob.com/php/func-array-list.html)     | 把数组中的值赋给一些数组变量。                               |
| [natcasesort()](http://www.runoob.com/php/func-array-natcasesort.html) | 用"自然排序"算法对数组进行不区分大小写字母的排序。           |
| [natsort()](http://www.runoob.com/php/func-array-natsort.html) | 用"自然排序"算法对数组排序。                                 |
| [next()](http://www.runoob.com/php/func-array-next.html)     | 将数组中的内部指针向后移动一位。                             |
| [pos()](http://www.runoob.com/php/func-array-pos.html)       | current() 的别名。                                           |
| [prev()](http://www.runoob.com/php/func-array-prev.html)     | 将数组的内部指针倒回一位。                                   |
| [range()](http://www.runoob.com/php/func-array-range.html)   | 创建一个包含指定范围的元素的数组。                           |
| [reset()](http://www.runoob.com/php/func-array-reset.html)   | 将数组的内部指针指向第一个元素。                             |
| [rsort()](http://www.runoob.com/php/func-array-rsort.html)   | 对数值数组进行降序排序。                                     |
| [shuffle()](http://www.runoob.com/php/func-array-shuffle.html) | 把数组中的元素按随机顺序重新排列。                           |
| [sizeof()](http://www.runoob.com/php/func-array-sizeof.html) | count() 的别名。                                             |
| [sort()](http://www.runoob.com/php/func-array-sort.html)     | 对数值数组进行升序排序。                                     |
| [uasort()](http://www.runoob.com/php/func-array-uasort.html) | 使用用户自定义的比较函数对数组中的键值进行排序。             |
| [uksort()](http://www.runoob.com/php/func-array-uksort.html) | 使用用户自定义的比较函数对数组中的键名进行排序。             |
| [usort()](http://www.runoob.com/php/func-array-usort.html)   | 使用用户自定义的比较函数对数组进行排序。                     |