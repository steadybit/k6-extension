# Steadybit K6 Extension

This is a small extension for [K6](https://k6.io) to start steadybit experiments from within your K6 scripts.

[Full K6 Example using Steadybit](https://github.com/steadybit/examples/tree/main/loadtest/k6-start-experiment)

Example Usage:
```javascript
import steadybit from 'https://raw.githubusercontent.com/steadybit/k6-extension/v1.0.0/index.js';

//run your k6 script like this
// STEADYBIT_ACCESS_KEY="39rTxhsl.******" k6 run --vus=1 --duration=60s script.js


export function setup() {
    let execution = steadybit.start('SHOP-190');
    console.log(`Started Steadybit Experiment SHOP-190`);
    return { execution };
}

export function teardown({ execution }) {
    try {
        steadybit.verifyCompleted(execution);
    } catch (error) {
        console.error(`Steadybit Experiment failed: ${error}`);

        try {
            steadybit.cancel(execution);
        } catch (error) {
            console.warn('Failed to cancel Steadybit Experiment', error);
        }
    }
}
```
