# Better Reading of Senor Data

## Fredik was whack

For a little while I was working on setting up an RC Robot. I had a bunch of issues with really bad gittering.

The problem was the range that any give positing of the toggles was very wide.

To combat this I made use of a running average.

The principle was simple enough to pick up on.

Use a list of readings to find an average over time rather than just what is currently coming in in that loop.

The setup currently is

```
#define ROLLING_SIZE 10
int rolling_acceleration[ROLLING_SIZE] = {0,0,0,0,0,0,0,0,0,0};
int rolling_direction[ROLLING_SIZE] = {0,0,0,0,0,0,0,0,0,0};

// Pin setup omitted

void loop() {
    // ch2, ch4 read in data
    for(int i=0; i < 10; i++){
        int acc_tmp = rolling_acceleration[i];
        int dir_tmp = rolling_direction[i];
        rolling_acceleration[i] = ch2;
        rolling_direction[i] = ch4;
        ch2 = acc_tmp;
        ch4 = dir_tmp;
    }
}

```

There did not appear to be a good way to read the size of an array so I just hard coded it.
