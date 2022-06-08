### Python Version (Anaconda)

install anaconda

```shell
wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh
bash Anaconda3-2020.07-Linux-x86_64.sh
```

create a python3.7 environment

```shell
conda create -n python37 python=3.7
```

inwstall a specific package

```shell
conda install -n python37 scipy
```

list all environments

```shell
conda env list
```

activate an environment

```shell
conda activate python37
```

deactivate an environment

```shell
conda deactivate
```



### 查看文件行数

```shell
wc -l <filename>
```



### YCSB generation

```shell
cd ~/Desktop/Heterogeneous_Memory/ERT/index-microbench
conda activate python27
YCSB/bin/ycsb load basic -P workload_spec/workloada -s > workloads/ycsb_txn_randint_workloada_50M
```



### Docker 使用

启动docker `docker start <ID/docker_name>`

查看已启动docker `docker ps -n 5`

停止docker `docker stop` / `docker kill`

重启docker `docker restart <ID/docker_name>`



### Haskell学习

不能用tab，必须用空格，对齐很严格

https://www.w3cschool.cn/hsriti/

```haskell
-- 注释是 --
-- 表示输入一个Block 类型和一个(Int, Int, Int)类型的tuple，输出一个GCStmt
-- 第一行声明transBlk函数，然后定义该函数，函数内部使用pattern matching
transBlk :: Block -> (Int, Int, Int) -> GCStmt
transBlk blk ctr =
  case blk of
  [] -> GCAssume GCTrue
  [x] -> transStmt x ctr
  (x:xs) -> GCSeq (transStmt x ctr) (transBlk xs ctr)
```



### Markdown

New page command

```markdown
<div style="page-break-after: always"></div>
```



### Tmux

```shell
tmux # enter tmux terminal
# connect to the server and close the terminal
tmux ls # watch how many sessions are alive
tmux attach -t <session_num> # recover to the session
```



### rsync

```shell
rsync -azr ./spotify-challenge/ kw754@node.zoo.cs.yale.edu:~/spotify-challenge/
rsync -azr -e "ssh -p 2100" ./spotify-challenge/  wangke@101.6.96.180:~/spotify-challenge/ # specify port
```





## Rust

Rust’s build system and package manager: **Cargo**

Creating a Project with Cargocargo new <project name>

- Creating a Project  `cargo new <project name>`
- We can build a project using `cargo build` , build a release version using `cargo build --release`.
- We can build and run a project in one step using `cargo run`.
- We can build a project without producing a binary to check for errors using `cargo check`.



`Option` and `Result`:

`Option`: 1. Some  2. None

```rust
let val: Option<u32> = get_some_val();

match val {
    Some(num) => println!("val is: {}", num),
    None => println!("val is None")
}
```

 `Result`: 1. Ok  2. Err

```rust
let sr: Result<u32, &str> = Ok(123); //or Err("You are wrong");

match sr {
    Ok(v) => println!("sr value: {}", v),
    Err(e) => println!("sr is error {}", e)
}
```

`?` question mark: return Err for the function whenever an Err occurs.

```rust
fn srst() -> Option<u32> {
    let sr: u32 = rs.get_u32_result()?;
    println!("sr is ok: {}", sr);
    
    let st: u8 = rs.get_u8_result()?;
    println!("st is ok: {}", st)
    
    Ok(sr + st as u32);
}

let sum: Option<u32> = srst();
```

 



How to alloc memory?

```rust
use std::alloc::{alloc, dealloc, Layout};

unsafe {
    let layout = Layout::new::<u16>();
    let ptr = alloc(layout);

    *(ptr as *mut u16) = 42;
    assert_eq!(*(ptr as *mut u16), 42);

    dealloc(ptr, layout);
}
```





## Python



### How to get a function name as a string?

Using `__name__`

```python
import time
time.time.__name__ 
```





## Jupiter Notebook

### Add a kernel

https://queirozf.com/entries/jupyter-kernels-how-to-add-change-remove

- Activate the virtualenv, e.g., `conda activate python37`.

- Install jupyter in the virtualenv

  ```
  (your-venv)$ pip install jupyter --user
  ```

- Add the virtualenv as a jupyter kernel, e.g, replace `your-env` as `python37`.

  ```
  (your-venv)$ ipython kernel install --name "your-venv" --user
  ```

- You can now select the created kernel `your-env` when you start Jupyter.



### Enable autocompletion

```shell
pip install jupyter_contrib_nbextensions # Install the python package
jupyter contrib nbextension install --user # Install javascript and css files
# install bnextensions_configurator
pip3 install jupyter_nbextensions_configurator
jupyter nbextensions_configurator enable --user
```

Restart jupyter (Note: not restart kernel)

https://blog.csdn.net/qq_37486501/article/details/104440755