
<a name="0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter"></a>

# Module `0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364::Counter`



-  [Resource `CounterHolder`](#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder)
-  [Constants](#@Constants_0)
-  [Function `init_counter`](#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_init_counter)
-  [Function `get_counter`](#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_get_counter)
-  [Function `inc_counter`](#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_inc_counter)


<pre><code><b>use</b> <a href="">0x1::signer</a>;
</code></pre>



<a name="0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder"></a>

## Resource `CounterHolder`



<pre><code><b>struct</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder">CounterHolder</a> <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>counter: u8</code>
</dt>
<dd>

</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_ENOT_INIT"></a>



<pre><code><b>const</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_ENOT_INIT">ENOT_INIT</a>: u64 = 0;
</code></pre>



<a name="0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_init_counter"></a>

## Function `init_counter`



<pre><code><b>public</b> <b>fun</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_init_counter">init_counter</a>(account: <a href="">signer</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> entry <b>fun</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_init_counter">init_counter</a>(account: <a href="">signer</a>)
<b>acquires</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder">CounterHolder</a> {
    <b>let</b> counter: u8 = 0;
    <b>let</b> account_addr = <a href="_address_of">signer::address_of</a>(&account);
    <b>if</b> (!<b>exists</b>&lt;<a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder">CounterHolder</a>&gt;(account_addr)) {
        <b>move_to</b>(&account, <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder">CounterHolder</a> {
            counter,
        })
    } <b>else</b> {
        <b>let</b> old_counter_holder = <b>borrow_global_mut</b>&lt;<a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder">CounterHolder</a>&gt;(account_addr);
        old_counter_holder.counter = 0;
    }
}
</code></pre>



</details>

<a name="0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_get_counter"></a>

## Function `get_counter`



<pre><code><b>public</b> <b>fun</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_get_counter">get_counter</a>(account: <a href="">signer</a>): u8
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_get_counter">get_counter</a>(account: <a href="">signer</a>): u8 <b>acquires</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder">CounterHolder</a> {
    <b>let</b> account_addr = <a href="_address_of">signer::address_of</a>(&account);
    <b>let</b> counter = <b>borrow_global_mut</b>&lt;<a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder">CounterHolder</a>&gt;(account_addr);
    counter.counter
}
</code></pre>



</details>

<a name="0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_inc_counter"></a>

## Function `inc_counter`



<pre><code><b>public</b> <b>fun</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_inc_counter">inc_counter</a>(account: <a href="">signer</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> entry <b>fun</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_inc_counter">inc_counter</a>(account: <a href="">signer</a>)
<b>acquires</b> <a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder">CounterHolder</a> {
    <b>let</b> account_addr = <a href="_address_of">signer::address_of</a>(&account);
    <b>let</b> counter = <b>borrow_global_mut</b>&lt;<a href="Counter.md#0xaf49ab5799b9cef57c363337aa8b71ae3a9ee91512005c3517c95f2944ee1364_Counter_CounterHolder">CounterHolder</a>&gt;(account_addr);
    counter.counter = counter.counter + 1
}
</code></pre>



</details>
