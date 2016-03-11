---
layout: post
title: php 生成不重复数组
date: 2012-08-27 16:02:00
category: blog
description: php 生成不重复数组
---

<?php


function test($num) {

    for($i=0;$i<$num;$i++) {

        $a[] = rand(0,9);
    }

    for($i=0;$i<$num-1;$i++) {

        for($j=$i+1;$j<$num;$j++) {

            if($a[$i] == $a[$j]) {

                $n = 0;

                while($n == 0) {

                    $a[$j] = rand(0,9);

                    for($s=0;$s<$j;$s++) {

                        if($a[$j] == $a[$s]) {

                            break;

                        }
                    }


                    if($s == $j) {

                        $n =1;
                    }else {

                    $n = 0;

                    }

                }

            }


        }

    }

    return $a;
}

print_r(test(5));

?>