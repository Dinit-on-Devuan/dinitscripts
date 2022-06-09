#!/bin/sh

## Debian/Devuan urandom (random-seed) script for Dinit
## Based on Debian/Devuan urandom sysvinit script
## Author: Mobin Aydinfar <mobin@mobintestserver.ir>
## LISENCE: GPLv3 or later
## Copyright (C) 2022 Dinit on Devuan project: https://git.mobintestserver.ir/Dinit_on_Devuan

## Define $SAVEDFILE
SAVEDFILE=/var/lib/urandom/random-seed

## Test /dev/urandom
[ -c /dev/urandom ] || exit 0

## Define $PATH
PATH=/sbin:/bin

## Define $POOLBYTES
if ! POOLBYTES=$((
   ($(cat /proc/sys/kernel/random/poolsize 2>/dev/null) + 7) / 8
)) ; then
    POOLBYTES=512
fi

## Define 'save' & 'load' commands
case "$1" in
  load)
    echo $(date) "Initializing random number generator..."
    (
      date +%s.%N
      if [ -f "$SAVEDFILE" ]
      then
        cat "$SAVEDFILE"
      fi
    ) >/dev/urandom

    umask 077
    dd if=/dev/urandom of=$SAVEDFILE bs=$POOLBYTES count=1 > /dev/null 2>&1
    ES=$?
    umask 022
    if [ $ES -eq 0 ] ; then
       echo $(date) "Initializing random number generator has return 0: Done!"
    else
       echo $(date) "Initializing random number generator has return $ES: FAILED!"
    fi
    ;;

  save)
    echo $(date) "Saving random seed..."
    umask 077
    dd if=/dev/urandom of=$SAVEDFILE bs=$POOLBYTES count=1 > /dev/null 2>&1
    ES=$?
    if [ $ES -eq 0 ] ; then
      echo $(date) "Saving random seed has return 0: Done!"
    else
      echo $(date) "Saving random seed has return $ES: FAILED!"
    fi
    ;;

  restart|reload|force-reload|status)
    echo "Error: argument '$1' not supproted!" >&2
    exit 3
    ;;

  *)
    echo "Urandom for Dinit. Don't using it DIRECTLY! Its must be managed by dinit(8)" >&2
    echo "Usage: urandom for dinit start|stop" >&2
    exit 3
    ;;
esac
