# ⚡ Cache-Aware CPU Scheduler Simulator

This project implements a **multi-CPU scheduler** with **cache-aware execution modeling** in Python.  
It simulates how jobs interact with CPU caches, considering **cache warmup times**, **working set sizes**, **affinity constraints**, and **scheduling policies** (centralized vs per-CPU distributed queues).  

The simulator demonstrates how cache locality and scheduling decisions impact system throughput and performance.

---

## 🚀 Features
- 🖥️ Supports **multi-core CPU scheduling**  
- 🧮 Models **cache warmup time & warm/cold execution rates**  
- 🏷️ Jobs defined with **runtime & working set sizes**  
- 🎯 Supports **CPU affinity constraints**  
- 🔄 Configurable **centralized or per-CPU distributed queues**  
- 👀 Tracing options for **time left, cache state, and scheduling decisions**  
- 📊 Reports **CPU utilization** and **cache warm hit ratio**  

---

## 🛠️ Usage

Run the simulator:

```bash
python cache_scheduler.py [options]
````

### Options

* `-s`, `--seed` → Random seed (default = 0)
* `-j`, `--job_num` → Number of jobs (default = 3)
* `-R`, `--max_run` → Max runtime of jobs (default = 100)
* `-W`, `--max_wset` → Max working set size (default = 200)
* `-L`, `--job_list` → Custom job list in format `name:runtime:wset`
* `-A`, `--affinity` → CPU affinity list (`a:0.1.2,b:0.1`)
* `-p`, `--per_cpu_queues` → Enable per-CPU queues (default = centralized)
* `-n`, `--num_cpus` → Number of CPUs (default = 2)
* `-q`, `--quantum` → Time slice length (default = 10)
* `-P`, `--peek_interval` → Peek interval for job stealing (default = 30, 0 = off)
* `-w`, `--warmup_time` → Cache warmup time (default = 10)
* `-r`, `--warm_rate` → Speedup factor with warm cache (default = 2)
* `-M`, `--cache_size` → Cache size (default = 100)
* `-o`, `--rand_order` → Assign CPUs in random order
* `-t`, `--trace` → Enable basic tracing (job execution)
* `-T`, `--trace_time_left` → Show remaining runtime per job
* `-C`, `--trace_cache` → Show cache status (warm/cold)
* `-S`, `--trace_sched` → Show scheduling queues
* `-c`, `--compute` → Show utilization and statistics

---

## 🧪 Examples

1. **Default run with 3 jobs, 2 CPUs**

```bash
python cache_scheduler.py -j 3 -n 2 -c
```

2. **Custom job list with cache warmup**

```bash
python cache_scheduler.py -L a:20:100,b:15:50,c:10:200 -n 2 -w 5 -r 3 -c
```

3. **Per-CPU scheduling with job stealing every 20 ticks**

```bash
python cache_scheduler.py -p -P 20 -j 4 -n 2 -c
```

4. **Enable full tracing**

```bash
python cache_scheduler.py -j 3 -n 2 -t -T -C -S
```

---

## 📊 Sample Output

```
ARG seed 0
ARG job_num 3
ARG num_cpus 2
ARG cache_size 100
ARG quantum 10

Job name:a run_time:20 working_set_size:100
Job name:b run_time:15 working_set_size:50
Job name:c run_time:10 working_set_size:200

Scheduler central queue: ['a', 'b', 'c']

Execution Trace:
  0   a [ 20] cache[w  ]  Q: b c
  1   a [ 18] cache[w  ]  Q: b c
...

Finished time 30

Per-CPU stats
  CPU 0  utilization 66.67 [ warm 50.00 ]
  CPU 1  utilization 33.33 [ warm 25.00 ]
```

---

## 📂 Project Structure

```
📁 Cache-Aware-CPU-Scheduler
│── cache_scheduler.py   # Main simulator code
│── README.md            # Documentation
```

---

## 👨‍💻 Author

* Hasan Zarook (2021-CE-58)

---

## 📜 License

This project is licensed under the **MIT License**.

```
