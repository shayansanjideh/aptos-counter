
<a name="0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter"></a>

# Module `0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9::Counter`



-  [Resource `CounterHolder`](#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder)
-  [Constants](#@Constants_0)
-  [Function `init_counter`](#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_init_counter)
-  [Function `get_counter`](#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_get_counter)
-  [Function `inc_counter`](#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_inc_counter)


<pre><code><b>use</b> <a href="">0x1::error</a>;
<b>use</b> <a href="">0x1::signer</a>;
</code></pre>



<a name="0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder"></a>

## Resource `CounterHolder`



<pre><code><b>struct</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a> <b>has</b> key
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


<a name="0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_ENOT_INIT"></a>



<pre><code><b>const</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_ENOT_INIT">ENOT_INIT</a>: u64 = 0;
</code></pre>



<a name="0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_init_counter"></a>

## Function `init_counter`



<pre><code><b>public</b> <b>fun</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_init_counter">init_counter</a>(account: <a href="">signer</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> entry <b>fun</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_init_counter">init_counter</a>(account: <a href="">signer</a>)
<b>acquires</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a> {
    <b>let</b> counter: u8 = 0;
    <b>let</b> account_addr = <a href="_address_of">signer::address_of</a>(&account);
    <b>if</b> (!<b>exists</b>&lt;<a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a>&gt;(account_addr)) {
        <b>move_to</b>(&account, <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a> {
            counter,
        })
    } <b>else</b> {
        <b>let</b> old_counter_holder = <b>borrow_global_mut</b>&lt;<a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a>&gt;(account_addr);
        old_counter_holder.counter = 0;
    }
}
</code></pre>



</details>

<a name="0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_get_counter"></a>

## Function `get_counter`



<pre><code><b>public</b> <b>fun</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_get_counter">get_counter</a>(addr: <b>address</b>): u8
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_get_counter">get_counter</a>(addr: <b>address</b>): u8 <b>acquires</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a> {
    <b>assert</b>!(<b>exists</b>&lt;<a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a>&gt;(addr), <a href="_not_found">error::not_found</a>(<a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_ENOT_INIT">ENOT_INIT</a>));
    *&<b>borrow_global</b>&lt;<a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a>&gt;(addr).counter
}
</code></pre>



</details>

<a name="0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_inc_counter"></a>

## Function `inc_counter`



<pre><code><b>public</b> <b>fun</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_inc_counter">inc_counter</a>(account: <a href="">signer</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> entry <b>fun</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_inc_counter">inc_counter</a>(account: <a href="">signer</a>)
<b>acquires</b> <a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a> {
    <b>let</b> account_addr = <a href="_address_of">signer::address_of</a>(&account);
    <b>let</b> counter = <b>borrow_global_mut</b>&lt;<a href="Counter.md#0xa905aa2b7734bfd044e9ef3cd10561b5e8d1dc1d6de2df6c35cfa2d2a3d544a9_Counter_CounterHolder">CounterHolder</a>&gt;(account_addr);
    counter.counter = counter.counter + 1
}
</code></pre>



</details>
