#!/bin/sh

## Recovery mode for dinit
## Author: Mobin Aydinfar <mobin@mobintestserver.ir>
## LISENCE: GPLv3 or later
## Dinit on Devuan Project https://git.mobintestserver.ir/Dinit_on_Devuan

## Print useful info
clear
echo "Welcome to recovery/resuce mode!"
echo "Dont panic! Your system failed to boot & Dinit loads recovery service & Single-user mode"

## Try to mount root as read-write filesystem
echo ""
echo "Trying to remounting root (/) as read-write filesystem... \cof"
/bin/mount -o remount,rw /
if [ $? -eq 0 ] ; then
  echo "Done!"
  else
  echo "FAILED! Your root is BROKEN!"
fi

## Try to set hostname from /etc/hostname
echo ""
echo "Trying to setting hostname from /etc/hostname... \cof"
/etc/dinit.d/scripts/hostname
if [ $? -eq 0 ] ; then
  echo "Done!"
  else
  echo "FAILED!"
fi

## Try to connect to internet via networking/ifupdown
## Disabled by default
#echo ""
#echo "Trying to enable networking interfaces... \cof"
#/etc/dinit.d/scripts/networking start
#if [ $? -eq 0 ] ; then
#  echo "Done!"
#  else
#  echo "FAIELD!"
#fi

## Print useful commands
echo ""
echo "Useful commands:"
echo "Remount root (/) as read-write: '/bin/mount -o remount,rw /'"
echo "Enable network interfaces: '/etc/dinit.d/scripts/networking start'"
echo "Enable ssh daemon: 'mkdir /run/sshd & /usr/sbin/sshd &'"
echo "Enable dbus-daemon: '/etc/dinit.d/scripts/dbus-pre & dbus-daemon --system --nofork --nopidfile --print-address &'"
echo "Enable NetworkManager (NEED dbus-daemon): 'NetworkManager'"
echo "You can read useful commands at /run/help file: 'cat /run/help'"

## Print useful commands at file
echo "Useful commands on recovery/rescue mode" > /run/help
echo "Remount root(/) as read-write: '/bin/mount -o remount,rw /'" >> /run/help
echo "Enable network interfaces: '/etc/dinit.d/scripts/networking start'" >> /run/help
echo "Enable ssh daemon 'mkdir /run/sshd & /usr/sbin/sshd &'" >> /run/help
echo "Enable dbus-daemon: '/etc/dinit.d/scripts/dbus-pre & dbus-daemon --system --nofork --nopidfile --print-address &'" >> /run/help
echo "Enable NetworkManager (NEED dbus-daemon): 'NetworkManager'" >> /run/help

SHEEL="/bin/bash"
## Load $SHEEL
echo ""
echo "Now, you have a shell for restore system"
echo ""$SHEEL" is loaded. Good Luck :)"
echo "NOTE: Dont use 'exit' command. rebooting system via 'reboot' or shuting down system via 'poweroff'! 'exit' command has buggy!"
exec $SHEEL
