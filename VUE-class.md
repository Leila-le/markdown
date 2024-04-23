range_start() {
            console.log(this.timeFilter);
            watch(
                () => this.timeFilter, // 监听 range_start 的变化
                (newVal, oldVal) => {
                    // 回调函数，参数为新值和旧值
                    console.log("range_start 发生变化");
                    console.log("新值:", newVal);
                    console.log("旧值:", oldVal);
                    this.drawCharts();
                }, {immediate: true}
            );
        }
