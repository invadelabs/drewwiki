---
title: LircConfig-MythTV+mplayer
layout: default
---

mythtv;

    begin
    prog = mythtv
    button = 2
    repeat = 2
    config = Up
    end

    begin
    prog = mythtv
    button = 5
    repeat = 2
    config = Down
    end

    begin
    prog = mythtv
    button = 4
    repeat = 2
    config = Left
    end

    begin
    prog = mythtv
    button = 6
    repeat = 2
    config = Right
    end

    # OK/Select
    begin
    prog = mythtv
    button = 1
    config = Space
    end

    # Escape/Exit/Back
    begin
    prog = mythtv
    button = 3
    config = Esc
    end

    # Bring up Options Menu
    begin
    prog = mythtv
    button = 7
    config = M
    end

    # Pause
    begin
    prog = mythtv
    button = play
    repeat = 2
    config = P
    end

    # Fast forward (30 sec default)
    begin
    prog = mythtv
    button = ff
    repeat = 2
    config = >
    end

    # Rewind (10 sec default)
    begin
    prog = mythtv
    button = rewind
    repeat = 2
    config = <
    end

    # Record
    begin
    prog = mythtv
    button = rec
    repeat = 2
    config = R
    end

    # Delete
    begin
    prog = mythtv
    button = 9
    repeat = 2
    config = D
    end

    # Scroll up
    begin
    prog = mythtv
    button = ch_up
    repeat = 2
    config = PageUp
    end

    # Scroll down
    begin
    prog = mythtv
    button = ch_down
    repeat = 2
    config = PageDown
    end

    # Bring up OSD info
    begin
    prog = mythtv
    button = 8
    repeat = 2
    config = I
    end

    # Commerical Skip
    begin
    prog = mythtv
    button = 0
    repeat = 2
    config = z
    end
