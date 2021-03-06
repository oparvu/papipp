libpapipp
=========
A C++ wrapper around libpapi



Example
-------
```c++
    papi::event_set<PAPI_TOT_INS, PAPI_TOT_CYC, PAPI_BR_MSP, PAPI_L1_DCM> events;
    events.start_counters();

    {
        std::vector<int> v = {{11, 7, 5, 3, 1}};
        std::sort(std::begin(v), std::end(v));
    }

    events.stop_counters();

    // accessing counters via at<EventIndex>()
    std::cout << events.at<0>().counter() / static_cast<double>(events.at<1>().counter()) << " insns per cycle\n";

    // or via .get<EventCode>()
    std::cout << events.get<PAPI_L1_DCM>().counter() << " l1 dcache misses\n"
              << events.get<PAPI_BR_MSP>().counter() << " branch misses" << std::endl;
```

Output
------
```
0.291125 insns per cycle
181 l1 dcache misses
101 branch misses
```
